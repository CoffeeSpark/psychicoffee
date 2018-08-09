<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>新增著作</el-breadcrumb-item>
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
                    <el-form-item label="名称">
                        <el-input v-model="form.p_name" placeholder="著作名称"></el-input>
                    </el-form-item>
                    <el-form-item label="作者">
                        <el-input v-model="form.p_author" placeholder="作者姓名"></el-input>
                    </el-form-item>
                    <el-form-item label="ISBN号">
                        <el-input v-model="form.ISBN" placeholder="请输入ISBN号"></el-input>
                    </el-form-item>
                    <el-form-item label="出版社">
                        <el-input v-model="form.publisher" placeholder="请填写出版社名"></el-input>
                    </el-form-item>
                    <el-form-item label="著作类型">
                        <el-select v-model="form.p_category" placeholder="请选择著作类型">
                            <el-option label="科技专著" value="科技专著"></el-option>
                            <el-option label="其他" value="其他"></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="出版日期">
                        <el-col :span="11">
                            <el-date-picker v-model="form.pub_date" type="date" placeholder="选择日期"></el-date-picker>
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
                    <el-form-item label="书的封面">
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
                            <div slot="tip" class="el-upload__tip">bmp/png/jpg格式</div>
                        </el-upload>
                    </el-form-item>
                    <el-form-item label="CIP数据页面">
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
        name: 'Publication',
        data () {
            return {
                labelPosition: 'right',
                fileList: [],
                form: {
                    p_name: '',
                    p_author: '',
                    ISBN: '',
                    publisher: '',
                    p_category: '',
                    pub_date: '',
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
                    this.form.p_name = '',
                    this.form.p_author = '',
                    this.form.ISBN = '',
                    this.form.publisher = '',
                    this.form.p_category = '',
                    this.form.pub_date = '',
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
