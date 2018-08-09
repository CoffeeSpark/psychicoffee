<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>新增项目</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="container">
            <div class="form-box">
                <el-radio-group v-model="labelPosition" size="small">
                    <el-radio-button label="left">左对齐</el-radio-button>
                    <el-radio-button label="right">右对齐</el-radio-button>
                    <el-radio-button label="top">顶部对齐</el-radio-button>
                </el-radio-group>
                <div style="margin: 20px;"></div>
                <el-form ref="form" :label-position="labelPosition" :inline="false" :model="form" label-width="200px">
                    <el-form-item label="名称">
                        <el-input v-model="form.pj_name" placeholder="项目名称"></el-input>
                    </el-form-item>
                    <el-form-item label="项目编号">
                        <el-input v-model="form.pj_num" placeholder="请不要填写财务编号，没有的填无"></el-input>
                    </el-form-item>
                    <el-form-item label="负责人">
                        <el-input v-model="form.leader" placeholder="负责人"></el-input>
                    </el-form-item>
                    <el-form-item label="来源">
                        <el-input v-model="form.source" placeholder="来源"></el-input>
                    </el-form-item>
                    <el-form-item label="是否由校内单位分解而来">
                        <el-input v-model="form.dividing" placeholder="是否由校内单位分解而来"></el-input>
                    </el-form-item>
                    <el-form-item label="类型">
                        <el-select v-model="form.pj_category" placeholder="请选择类型">
                            <el-option label="..." value="..."></el-option>
                            <el-option label="..." value="..."></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="总经费（万元）">
                        <el-input v-model="form.expenditure" placeholder="请填写数字，如100.5"></el-input>
                    </el-form-item>
                    <el-collapse v-model="project_fee" @change="handleChange">
                        <el-collapse-item title="点击填写每年经费详情">
                            <el-form ref="form" :label-position="labelPosition" :inline="false" :model="form" label-width="150px">
                                <el-form-item label="所属年份">
                                    <el-date-picker v-model="form.belong_year" type="year" placeholder="选择年"></el-date-picker>
                                </el-form-item>
                                <el-form-item label="当年经费（万元）">
                                    <el-input v-model="form.year_fee" placeholder="请填写数字，如100.5"></el-input>
                                </el-form-item>
                                <el-form-item label="备注">
                                    <el-input v-model="form.commentary" placeholder="备注"></el-input>
                                </el-form-item>
                            </el-form>
                        </el-collapse-item>
                    </el-collapse>
                    <el-form-item label="参加人">
                        <el-input v-model="form.group_members" placeholder="参加人"></el-input>
                    </el-form-item>
                    <el-form-item label="起始年月">
                        <el-col :span="11">
                            <el-date-picker v-model="form.start_time" type="month" placeholder="选择年月"></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="终止年月">
                        <el-col :span="11">
                            <el-date-picker v-model="form.end_time" type="month" placeholder="选择年月"></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="备注">
                        <el-input v-model="form.commentary" placeholder="备注"></el-input>
                    </el-form-item>
                    <el-form-item label="项目附件">
                        <el-upload
                            id="uploadFile"
                            action="http://127.0.0.1:3303/api/user/file_upload"
                            name="files"
                            :on-preview="handlePreview"
                            :on-remove="handleRemove"
                            :before-remove="beforeRemove"
                            :limit="1"
                            :on-exceed="handleExceed"
                            :file-list="fileList"
                            show-file-list
                            >
                            <el-button type="primary">点击上传</el-button>
                            <div slot="tip" class="el-upload__tip">doc/docx/pdf格式</div>
                        </el-upload>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="onSubmit">提交</el-button>
                        <el-button @click="onCancel">重置</el-button>
                    </el-form-item>
                </el-form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'project',
        data () {
            return {
                labelPosition: 'right',
                fileList: [],
                form: {
                    pj_name: '',
                    pj_num: '',
                    leader: '',
                    source: '',
                    dividing: '',
                    pj_category: '',
                    expenditure: '',
                    group_members: '',
                    start_time: '',
                    end_time:'',
                    commentary: ''
                }
            }
        },
        methods: {
            onSubmit() {
                // this.$message.success('提交成功！');
                console.log(JSON.stringify(this.form));
            },
            onCancel () {
                this.$confirm('确定重置所有输入？')
                .then(_ => { // 点击确认，重置
                    this.form.pj_name = '',
                    this.form.pj_num = '',
                    this.form.leader = '',
                    this.form.source = '',
                    this.form.dividing = '',
                    this.form.pj_category = '',
                    this.form.expenditure = '',
                    this.form.group_members = '',
                    this.form.start_time = '',
                    this.form.end_time = '',
                    this.form.commentary = ''
                }) // 否则不重置
                .catch(_ => {});
            },
            handleRemove(file, fileList) {
                console.log(file, fileList);
            },
            handlePreview(file) {
                console.log(JSON.stringify(file));
            },
            handleExceed(files, fileList) {
                this.$message.warning(`当前限制选择 1 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
            },
            beforeRemove(file, fileList) {
                return this.$confirm(`确定移除 ${ file.name }？`);
            }
        }
    }
</script>
<style>
/* 重写文件上传框样式 */
.el-upload--text{
    height: 100px;
}
</style>


<el-form-item label="每年经费详情:所属年份">
    
</el-form-item>

