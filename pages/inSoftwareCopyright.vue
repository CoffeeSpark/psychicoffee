<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>新增软件著作权</el-breadcrumb-item>
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
                    <el-form-item label="软件名称">
                        <el-input v-model="form.sc_name" placeholder="软件名称"></el-input>
                    </el-form-item>
                    <el-form-item label="软件登记号">
                        <el-input v-model="form.sc_num" placeholder="软件登记号"></el-input>
                    </el-form-item>
                    <el-form-item label="是否独立完成">
                        <el-input v-model="form.independence" placeholder="是否独立完成"></el-input>
                    </el-form-item>
                    <el-form-item label="完成单位">
                        <el-input v-model="form.unit" placeholder="完成单位"></el-input>
                    </el-form-item>
                    <el-form-item label="完成人">
                        <el-input v-model="form.sc_inventor" placeholder="完成人"></el-input>
                    </el-form-item>
                    <el-form-item label="首次发表时间">
                        <el-col :span="11">
                            <el-date-picker v-model="form.apply_time" type="date" placeholder="选择日期"></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="批准时间">
                        <el-col :span="11">
                            <el-date-picker v-model="form.authorize_time" type="date" placeholder="选择日期"></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="所属年份">
                        <el-col :span="11">
                            <el-date-picker v-model="form.belong_year" type="year" placeholder="选择年"></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="备注">
                        <el-input v-model="form.commentary" placeholder="备注"></el-input>
                    </el-form-item>
                    <el-form-item label="登记证书">
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
        name: 'SoftwareCopyright',
        data () {
            return {
                labelPosition: 'right',
                fileList: [],
                form: {
                    sc_name: '',
                    sc_num: '',
                    independence: '',
                    unit: '',
                    sc_inventor: '',
                    apply_time: '',
                    authorize_time: '',
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
                    this.form.sc_name = '',
                    this.form.sc_num = '',
                    this.form.independence = '',
                    this.form.unit = '',
                    this.form.sc_inventor = '',
                    this.form.apply_time = '',
                    this.form.authorize_time = '',
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