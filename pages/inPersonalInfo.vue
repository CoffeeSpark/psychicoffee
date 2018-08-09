<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>编辑我的个人信息</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="container">
                <div style="margin: 40px;"></div>
                <el-form :inline="true" :model="formInline" label-position="left" label-width="120px">
                    <el-form-item label="姓名">
                        <el-col :span="22">
                            <el-input v-model="form.tch_name" :disabled="true" placeholder="教师姓名" ></el-input>
                        </el-col>                    
                    </el-form-item>
                    <el-form-item label="人事编号">
                        <el-col :span="22">
                            <el-input v-model="form.tch_id" :disabled="true" placeholder="教师人事编号"></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="性别">
                        <el-col :span="22">
                            <el-input v-model="form.gender" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="出生日期">
                        <el-col :span="22">
                            <el-date-picker v-model="form.birthday" type="date" ></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="籍贯">
                        <el-col :span="22">
                            <el-input v-model="form.nativity" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="民族">
                        <el-col :span="22">
                            <el-input v-model="form.nation" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="政治面貌">
                        <el-col :span="22">
                            <el-input v-model="form.politics_status" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="身份证号">
                        <el-col :span="22">
                            <el-input v-model="form.ID_num" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="职工类别">
                        <el-col :span="22">
                            <el-input v-model="form.work_category" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="进校时间">
                        <el-col :span="22">
                            <el-date-picker v-model="form.entry_time" type="month" ></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="学历">
                        <el-col :span="22">
                            <el-input v-model="form.edu_background" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="专业">
                        <el-col :span="22">
                            <el-input v-model="form.major" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="学位">
                        <el-col :span="22">
                            <el-input v-model="form.dregree" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="学位获得时间">
                        <el-col :span="22">
                            <el-date-picker v-model="form.dregree_time" type="month" ></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="授予单位">
                        <el-col :span="22">
                            <el-input v-model="form.award_by" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="参加工作时间">
                        <el-col :span="22">
                            <el-date-picker v-model="form.work_start" type="month" ></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="专技职称">
                        <el-col :span="22">
                            <el-input v-model="form.pro_title" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="专技时间">
                        <el-col :span="22">
                            <el-date-picker v-model="form.pro_time" type="year" ></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="专业级别">
                        <el-col :span="22">
                            <el-input v-model="form.pro_level" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="定级时间">
                        <el-col :span="22">
                            <el-date-picker v-model="form.settle_time" type="month" ></el-date-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="电子邮箱">
                        <el-col :span="22">
                            <el-input v-model="form.email" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="联系电话">
                        <el-col :span="22">
                            <el-input v-model="form.phone" ></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="备注">
                        <el-col :span="22">
                            <el-input v-model="form.commentary" placeholder="备注"></el-input>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="个人简介">
                        <div class="edit_container">
                            <quill-editor v-model="form.resume" ></quill-editor>
                        </div>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="onSubmit">提交</el-button>
                        <el-button @click="onCancel">重置</el-button>
                    </el-form-item>
                </el-form>
            </div>
        </div>
</template>

<script>
    import { quillEditor } from 'vue-quill-editor' //调用编辑器
    export default {
        name: 'PersonalInfo',
        data () {
            return {
                labelPosition: 'right',
                fileList: [],
                form: {
                    tch_name: '',
                    tch_id: '',
                    gender: '',
                    birthday: '',
                    nativity: '',
                    nation: '',
                    politics_status: '',
                    ID_num: '',
                    work_category: '',
                    entry_time: '',
                    edu_background: '',
                    major: '',
                    degree: '',
                    degree_time: '',
                    award_by: '',
                    work_start: '',
                    pro_title: '',
                    pro_time: '',
                    pro_level: '',
                    settle_time: '',
                    email: '',
                    phone: '',
                    commentary: '',
                    resume: ''
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
                    this.form.tch_name = '',
                    this.form.tch_id = '',
                    this.form.gender = '',
                    this.form.birthday = '',
                    this.form.nativity = '',
                    this.form.nation = '',
                    this.form.politics_status = '',
                    this.form.ID_num = '',
                    this.form.work_category = '',
                    this.form.entry_time = '',
                    this.form.edu_background = '',
                    this.form.major = '',
                    this.form.degree = '',
                    this.form.degree_time = '',
                    this.form.award_by = '',
                    this.form.work_start = '',
                    this.form.pro_title = '',
                    this.form.pro_time = '',
                    this.form.pro_level = '',
                    this.form.settle_time = '',
                    this.form.email = '',
                    this.form.phone = '',
                    this.form.commentary = '',
                    this.form.resume = ''
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
