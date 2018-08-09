<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>新增论文</el-breadcrumb-item>
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
                        <el-input v-model="form.paper_name" placeholder="论文名称"></el-input>
                    </el-form-item>
                    <el-form-item label="作者">
                        <el-input v-model="form.author" placeholder="作者姓名"></el-input>
                    </el-form-item>
                    <el-form-item label="论文类型">
                        <el-select v-model="form.category" placeholder="请选择论文类型">
                          <el-option label="自然科学论文" value="自然科学论文"></el-option>
                          <el-option label="社会科学论文" value="社会科学论文"></el-option>
                          <el-option label="其他" value="其他"></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="论文收录类型">
                        <el-select v-model="form.in_category" placeholder="请选择收录类型">
                            <el-option label="SCI" value="SCI"></el-option>
                            <el-option label="中文核心" value="中文核心"></el-option>
                            <el-option label="其他" value="其他"></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="期刊/会议名称">
                        <el-input v-model="form.meeting_name" placeholder="期刊/会议名称"></el-input>
                    </el-form-item>
                    <el-form-item label="卷期页/会议时间地点">
                        <el-input v-model="form.time_place" placeholder="卷期页/会议时间地点"></el-input>
                    </el-form-item>
                    <el-form-item label="第一作者">
                        <el-input v-model="form.fir_author" placeholder="第一作者"></el-input>
                    </el-form-item>
                    <el-form-item label="通讯作者">
                        <el-input v-model="form.com_author" placeholder="通讯作者"></el-input>
                    </el-form-item>
                    <el-form-item label="备注">
                        <el-input v-model="form.commentary" placeholder="备注"></el-input>
                    </el-form-item>
                    <el-form-item label="所属年份">
                        <el-col :span="11">
                            <el-date-picker v-model="form.belong_year" type="year" placeholder="选择年"></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="附件">
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
                            <div slot="tip" class="el-upload__tip">选择pdf文件上传（不超过三个）</div>
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
        name: 'paper',
        data () {
            return {
                labelPosition: 'right',
                fileList: [],
                form: {
                    paper_name: '',
                    author: '',
                    category: '',
                    in_category: '',
                    meeting_name: '',
                    time_place: '',
                    fir_author: '',
                    com_author: '',
                    commentary: '',
                    belong_year: ''
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
                    this.form.paper_name = '',
                    this.form.author = '',
                    this.form.category = '',
                    this.form.in_category = '',
                    this.form.meeting_name = '',
                    this.form.time_place = '',
                    this.form.fir_author = '',
                    this.form.com_author = '',
                    this.form.commentary = '',
                    this.form.belong_year = ''
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
