<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>新增学术任职</el-breadcrumb-item>
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
                    <el-form-item label="任职者id">
                        <el-input v-model="form.personal_id" :disabled="true" placeholder="教师人事编号"></el-input>
                    </el-form-item>
                    <el-form-item label="姓名">
                        <el-input v-model="form.name" :disabled="true" placeholder="任职者姓名"></el-input>
                    </el-form-item>
                    <el-form-item label="类别">
                        <el-select v-model="form.category" placeholder="请选择类别">
                            <el-option label="期刊" value="期刊"></el-option>
                            <el-option label="学术组织" value="学术组织"></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="学术组织或期刊名">
                        <el-input v-model="form.organizations" placeholder="学术组织或期刊名"></el-input>
                    </el-form-item>
                    <el-form-item label="职务">
                        <el-input v-model="form.posistion" placeholder="职务"></el-input>
                    </el-form-item>
                    <el-form-item label="起始时间">
                        <el-date-picker v-model="form.start_time" type="date" placeholder="选择日期"></el-date-picker>
                    </el-form-item>
                    <el-form-item label="终止时间">
                        <el-date-picker v-model="form.end_time" type="date" placeholder="选择日期"></el-date-picker>
                    </el-form-item>
                    <el-form-item label="是否最重要">
                        <el-input v-model="form.importance" ></el-input>
                    </el-form-item>
                    <el-form-item label="证明文件">
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
                            <div slot="tip" class="el-upload__tip">doc/docx/pdf/jpg格式</div>
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
        name: 'AcademicPosition',
        data () {
            return {
                labelPosition: 'right',
                fileList: [],
                form: {
                    personl_id: '',
                    name: '',
                    category: '',
                    organizations: '',
                    position: '',
                    start_time: '',
                    end_time: '',
                    importance: ''
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
                    this.form.personl_id = '',
                    this.form.name = '',
                    this.form.category = '',
                    this.form.organizations = '',
                    this.form.position = '',
                    this.form.start_name = '',
                    this.form.end_time = '',
                    this.form.importance = ''
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