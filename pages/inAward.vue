<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>新增奖励</el-breadcrumb-item>
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
                <el-form ref="form" :label-position="labelPosition" :inline="false" :model="form" label-width="150px">
                    <el-form-item label="奖励名称">
                        <el-input v-model="form.a_name" placeholder="奖励名称"></el-input>
                    </el-form-item>
                    <el-form-item label="证书号">
                        <el-input v-model="form.a_num" placeholder="证书号"></el-input>
                    </el-form-item>
                    <el-form-item label="类别">
                        <el-input v-model="form.a_category" placeholder="请详细填写到获奖等级，如“国家科技进步二等奖”"></el-input>
                    </el-form-item>
                    <el-form-item label="获奖等级">
                        <el-select v-model="form.a_level" placeholder="请选择获奖等级">
                            <el-option label="国家科技进步二等奖" value="国家科技进步二等奖"></el-option>
                            <el-option label="..." value="..."></el-option>
                            <el-option label="其他" value="其他"></el-option>
                        </el-select>
                    </el-form-item>
                     <el-form-item label="参加人员">
                        <el-input v-model="form.group_members" placeholder="参加人员"></el-input>
                    </el-form-item>
                    <el-form-item label="承担单位">
                        <el-input v-model="form.department" placeholder="承担单位"></el-input>
                    </el-form-item>
                   <el-form-item label="授奖单位">
                        <el-input v-model="form.award_by" placeholder="授奖单位"></el-input>
                    </el-form-item>
                    <el-form-item label="所属年份">
                        <el-col :span="11">
                            <el-date-picker v-model="form.belong_year" type="year" placeholder="选择年"></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="备注">
                        <el-input v-model="form.commentary" placeholder="备注"></el-input>
                    </el-form-item>
                    <el-form-item label="项目说明">
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
                            show-file-list>
                            <el-button type="primary">点击上传</el-button>
                            <div slot="tip" class="el-upload__tip">doc/docx格式</div>
                        </el-upload>
                    </el-form-item>
                    <el-form-item label="证书">
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
                            <div slot="tip" class="el-upload__tip">bmp/png/jpg格式</div>
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
        name: 'Award',
        data () {
            return {
                labelPosition: 'right',
                fileList: [],
                form: {
                    a_name: '',
                    a_num: '',
                    a_category: '',
                    a_level: '',
                    group_menbers: '',
                    department: '',
                    award_by: '',
                    belong_year: '',
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
                    this.form.a_name = '',
                    this.form.a_num = '',
                    this.form.a_category = '',
                    this.form.a_level = '',
                    this.form.group_menbers = '',
                    this.form.department = '',
                    this.form.award_by = '',
                    this.form.belong_year = '',
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