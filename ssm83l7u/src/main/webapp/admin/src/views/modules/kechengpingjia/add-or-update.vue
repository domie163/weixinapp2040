<template>
  <div class="addEdit-block">
    <el-form
      class="detail-form-content"
      ref="ruleForm"
      :model="ruleForm"
      :rules="rules"
      label-width="80px"
	  :style="{backgroundColor:addEditForm.addEditBoxColor}"
    >
      <el-row>
      <el-col :span="12">
        <el-form-item class="select" v-if="type!='info'" label="课程名称" prop="kechengmingcheng">
          <el-select  @change="kechengmingchengChange" v-model="ruleForm.kechengmingcheng" placeholder="请选择课程名称">
            <el-option
                v-for="(item,index) in kechengmingchengOptions"
                v-bind:key="index"
                :label="item"
                :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <div v-else>
          <el-form-item class="input"v-if="ruleForm.kechengmingcheng" label="课程名称" prop="kechengmingcheng">
              <el-input v-model="ruleForm.kechengmingcheng" 
                placeholder="课程名称" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="课程类型" prop="kechengleixing">
          <el-input v-model="ruleForm.kechengleixing" 
              placeholder="课程类型" clearable  :readonly="ro.kechengleixing"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="课程类型" prop="kechengleixing">
              <el-input v-model="ruleForm.kechengleixing" 
                placeholder="课程类型" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="教师工号" prop="jiaoshigonghao">
          <el-input v-model="ruleForm.jiaoshigonghao" 
              placeholder="教师工号" clearable  :readonly="ro.jiaoshigonghao"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="教师工号" prop="jiaoshigonghao">
              <el-input v-model="ruleForm.jiaoshigonghao" 
                placeholder="教师工号" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="课程评分" prop="kechengpingfen">
          <el-input v-model="ruleForm.kechengpingfen" 
              placeholder="课程评分" clearable  :readonly="ro.kechengpingfen"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="课程评分" prop="kechengpingfen">
              <el-input v-model="ruleForm.kechengpingfen" 
                placeholder="课程评分" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="date" v-if="type!='info'" label="评价时间" prop="pingjiashijian">
            <el-date-picker
                format="yyyy 年 MM 月 dd 日"
                value-format="yyyy-MM-dd"
                v-model="ruleForm.pingjiashijian" 
                type="date"
                placeholder="评价时间">
            </el-date-picker> 
        </el-form-item>
        <div v-else>
          <el-form-item class="input" v-if="ruleForm.pingjiashijian" label="评价时间" prop="pingjiashijian">
              <el-input v-model="ruleForm.pingjiashijian" 
                placeholder="评价时间" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="24">  
        <el-form-item class="upload" v-if="type!='info' && !ro.kechengtupian" label="课程图片" prop="kechengtupian">
          <file-upload
          tip="点击上传课程图片"
          action="file/upload"
          :limit="3"
          :multiple="true"
          :fileUrls="ruleForm.kechengtupian?ruleForm.kechengtupian:''"
          @change="kechengtupianUploadChange"
          ></file-upload>
        </el-form-item>
        <div v-else>
          <el-form-item v-if="ruleForm.kechengtupian" label="课程图片" prop="kechengtupian">
            <img style="margin-right:20px;" v-bind:key="index" v-for="(item,index) in ruleForm.kechengtupian.split(',')" :src="item" width="100" height="100">
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="学号" prop="xuehao">
          <el-input v-model="ruleForm.xuehao" 
              placeholder="学号" clearable  :readonly="ro.xuehao"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="学号" prop="xuehao">
              <el-input v-model="ruleForm.xuehao" 
                placeholder="学号" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="学生姓名" prop="xueshengxingming">
          <el-input v-model="ruleForm.xueshengxingming" 
              placeholder="学生姓名" clearable  :readonly="ro.xueshengxingming"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="学生姓名" prop="xueshengxingming">
              <el-input v-model="ruleForm.xueshengxingming" 
                placeholder="学生姓名" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="班级" prop="banji">
          <el-input v-model="ruleForm.banji" 
              placeholder="班级" clearable  :readonly="ro.banji"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="班级" prop="banji">
              <el-input v-model="ruleForm.banji" 
                placeholder="班级" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      </el-row>
          <el-row>
            <el-col :span="24">
              <el-form-item v-if="type!='info'"  label="评价内容" prop="pingjianeirong">
                <editor 
                    style="min-width: 200px; max-width: 600px;"
                    v-model="ruleForm.pingjianeirong" 
                    class="editor" 
                    action="file/upload">
                </editor>
              </el-form-item>
              <div v-else>
                <el-form-item v-if="ruleForm.pingjianeirong" label="评价内容" prop="pingjianeirong">
                    <span v-html="ruleForm.pingjianeirong"></span>
                </el-form-item>
              </div>
            </el-col>
          </el-row>
      <el-form-item class="btn">
        <el-button v-if="type!='info'" type="primary" class="btn-success" @click="onSubmit">提交</el-button>
        <el-button v-if="type!='info'" class="btn-close" @click="back()">取消</el-button>
        <el-button v-if="type=='info'" class="btn-close" @click="back()">返回</el-button>
      </el-form-item>
    </el-form>
    

  </div>
</template>
<script>
// 数字，邮件，手机，url，身份证校验
import { isNumber,isIntNumer,isEmail,isPhone, isMobile,isURL,checkIdCard } from "@/utils/validate";
export default {
  data() {
    let self = this
    var validateIdCard = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!checkIdCard(value)) {
        callback(new Error("请输入正确的身份证号码"));
      } else {
        callback();
      }
    };
    var validateUrl = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isURL(value)) {
        callback(new Error("请输入正确的URL地址"));
      } else {
        callback();
      }
    };
    var validateMobile = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isMobile(value)) {
        callback(new Error("请输入正确的手机号码"));
      } else {
        callback();
      }
    };
    var validatePhone = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isPhone(value)) {
        callback(new Error("请输入正确的电话号码"));
      } else {
        callback();
      }
    };
    var validateEmail = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isEmail(value)) {
        callback(new Error("请输入正确的邮箱地址"));
      } else {
        callback();
      }
    };
    var validateNumber = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isNumber(value)) {
        callback(new Error("请输入数字"));
      } else {
        callback();
      }
    };
    var validateIntNumber = (rule, value, callback) => {
      if(!value){
        callback();
      } else if (!isIntNumer(value)) {
        callback(new Error("请输入整数"));
      } else {
        callback();
      }
    };
    return {
	  addEditForm: {"btnSaveFontColor":"#fff","selectFontSize":"14px","btnCancelBorderColor":"rgba(0, 0, 0, 1)","inputBorderRadius":"0px","inputFontSize":"14px","textareaBgColor":"#fff","btnSaveFontSize":"14px","textareaBorderRadius":"4px","uploadBgColor":"#fff","textareaBorderStyle":"solid","btnCancelWidth":"88px","textareaHeight":"120px","dateBgColor":"#fff","btnSaveBorderRadius":"25px","uploadLableFontSize":"14px","textareaBorderWidth":"1px","inputLableColor":"#606266","addEditBoxColor":"rgba(255, 255, 255, 1)","dateIconFontSize":"16px","btnSaveBgColor":"rgba(0, 123, 255, 1)","uploadIconFontColor":"rgba(0, 123, 255, 1)","textareaBorderColor":"rgba(65, 81, 100, 1)","btnCancelBgColor":"rgba(255, 255, 255, 1)","selectLableColor":"#606266","btnSaveBorderStyle":"solid","dateBorderWidth":"1px","dateLableFontSize":"14px","dateBorderRadius":"0px","btnCancelBorderStyle":"solid","selectLableFontSize":"14px","selectBorderStyle":"none none solid none","selectIconFontColor":"rgba(0, 123, 255, 1)","btnCancelHeight":"44px","inputHeight":"36px","btnCancelFontColor":"#606266","dateBorderColor":"rgba(65, 81, 100, 1)","dateIconFontColor":"rgba(0, 123, 255, 1)","uploadBorderStyle":"solid","dateBorderStyle":"none none solid none","dateLableColor":"#606266","dateFontSize":"14px","inputBorderWidth":"1px","uploadIconFontSize":"28px","selectHeight":"36px","inputFontColor":"rgba(96, 98, 102, 1)","uploadHeight":"120px","textareaLableColor":"#606266","textareaLableFontSize":"14px","btnCancelFontSize":"14px","inputBorderStyle":"none none solid none","btnCancelBorderRadius":"30px","inputBgColor":"rgba(255, 255, 255, 1)","inputLableFontSize":"14px","uploadLableColor":"#606266","uploadBorderRadius":"4px","btnSaveHeight":"44px","selectBgColor":"#fff","btnSaveWidth":"88px","selectIconFontSize":"20px","dateHeight":"36px","selectBorderColor":"rgba(65, 81, 100, 1)","inputBorderColor":"rgba(65, 81, 100, 1)","uploadBorderColor":"rgba(30, 144, 255, 1)","textareaFontColor":"#606266","selectBorderWidth":"1px","dateFontColor":"#606266","btnCancelBorderWidth":"1px","uploadBorderWidth":"1px","textareaFontSize":"14px","selectBorderRadius":"0px","selectFontColor":"#606266","btnSaveBorderColor":"rgba(255, 69, 0, 1)","btnSaveBorderWidth":"0px"},
      id: '',
      type: '',
      ro:{
	kechengmingcheng : false,
	kechengleixing : false,
	jiaoshigonghao : false,
	kechengpingfen : false,
	pingjianeirong : false,
	pingjiashijian : false,
	kechengtupian : false,
	xuehao : false,
	xueshengxingming : false,
	banji : false,
	userid : false,
      },
      ruleForm: {
        kechengmingcheng: '',
        kechengleixing: '',
        jiaoshigonghao: '',
        kechengpingfen: '',
        pingjianeirong: '',
        pingjiashijian: '',
        kechengtupian: '',
        xuehao: '',
        xueshengxingming: '',
        banji: '',
        userid: '',
      },
          kechengmingchengOptions: [],
      rules: {
          kechengmingcheng: [
          ],
          kechengleixing: [
          ],
          jiaoshigonghao: [
          ],
          kechengpingfen: [
                { validator: validateIntNumber, trigger: 'blur' },
          ],
          pingjianeirong: [
          ],
          pingjiashijian: [
          ],
          kechengtupian: [
          ],
          xuehao: [
          ],
          xueshengxingming: [
          ],
          banji: [
          ],
          userid: [
          ],
      }
    };
  },
  props: ["parent"],
  computed: {
  },
  created() {
	this.ruleForm.pingjiashijian = this.getCurDate()
	this.addEditStyleChange()
	this.addEditUploadStyleChange()
  },
  methods: {
    // 下载
    download(file){
      window.open(`${file}`)
    },
    // 初始化
    init(id,type) {
      if (id) {
        this.id = id;
        this.type = type;
      }
      if(this.type=='info'||this.type=='else'){
        this.info(id);
      }else if(this.type=='cross'){
        var obj = this.$storage.getObj('crossObj');
        for (var o in obj){
          if(o=='kechengmingcheng'){
            this.ruleForm.kechengmingcheng = obj[o];
	    this.ro.kechengmingcheng = true;
            continue;
          }
          if(o=='kechengleixing'){
            this.ruleForm.kechengleixing = obj[o];
	    this.ro.kechengleixing = true;
            continue;
          }
          if(o=='jiaoshigonghao'){
            this.ruleForm.jiaoshigonghao = obj[o];
	    this.ro.jiaoshigonghao = true;
            continue;
          }
          if(o=='kechengpingfen'){
            this.ruleForm.kechengpingfen = obj[o];
	    this.ro.kechengpingfen = true;
            continue;
          }
          if(o=='pingjianeirong'){
            this.ruleForm.pingjianeirong = obj[o];
	    this.ro.pingjianeirong = true;
            continue;
          }
          if(o=='pingjiashijian'){
            this.ruleForm.pingjiashijian = obj[o];
	    this.ro.pingjiashijian = true;
            continue;
          }
          if(o=='kechengtupian'){
            this.ruleForm.kechengtupian = obj[o];
	    this.ro.kechengtupian = true;
            continue;
          }
          if(o=='xuehao'){
            this.ruleForm.xuehao = obj[o];
	    this.ro.xuehao = true;
            continue;
          }
          if(o=='xueshengxingming'){
            this.ruleForm.xueshengxingming = obj[o];
	    this.ro.xueshengxingming = true;
            continue;
          }
          if(o=='banji'){
            this.ruleForm.banji = obj[o];
	    this.ro.banji = true;
            continue;
          }
          if(o=='userid'){
            this.ruleForm.userid = obj[o];
	    this.ro.userid = true;
            continue;
          }
        }
      }
      // 获取用户信息
      this.$http({
        url: `${this.$storage.get('sessionTable')}/session`,
        method: "get"
      }).then(({ data }) => {
        if (data && data.code === 0) {
          var json = data.data;
		if(json.xuehao!=''&&json.xuehao){
              		this.ruleForm.xuehao = json.xuehao
		}
		if(json.xueshengxingming!=''&&json.xueshengxingming){
              		this.ruleForm.xueshengxingming = json.xueshengxingming
		}
		if(json.banji!=''&&json.banji){
              		this.ruleForm.banji = json.banji
		}
        } else {
          this.$message.error(data.msg);
        }
      });
            this.$http({
              url: `option/kechengxinxi/kechengmingcheng`,
              method: "get"
            }).then(({ data }) => {
              if (data && data.code === 0) {
                this.kechengmingchengOptions = data.data;
              } else {
                this.$message.error(data.msg);
              }
            });
    },
    // 下二随
    kechengmingchengChange () {
      this.$http({
        url: `follow/kechengxinxi/kechengmingcheng?columnValue=`+ this.ruleForm.kechengmingcheng,
        method: "get"
      }).then(({ data }) => {
        if (data && data.code === 0) {
              if(data.data.kechengleixing){
                this.ruleForm.kechengleixing = data.data.kechengleixing
              }
        } else {
          this.$message.error(data.msg);
        }
      });
    },
    // 多级联动参数
    info(id) {
      this.$http({
        url: `kechengpingjia/info/${id}`,
        method: "get"
      }).then(({ data }) => {
        if (data && data.code === 0) {
        this.ruleForm = data.data;
	//解决前台上传图片后台不显示的问题
	let reg=new RegExp('../../../upload','g')//g代表全部
	this.ruleForm.pingjianeirong = this.ruleForm.pingjianeirong.replace(reg,'../../../ssm83l7u/upload');
        } else {
          this.$message.error(data.msg);
        }
      });
    },
    // 提交
    onSubmit() {
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}
      // ${column.compare}











      this.$refs["ruleForm"].validate(valid => {
        if (valid) {
          this.$http({
            url: `kechengpingjia/${!this.ruleForm.id ? "save" : "update"}`,
            method: "post",
            data: this.ruleForm
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.$message({
                message: "操作成功",
                type: "success",
                duration: 1500,
                onClose: () => {
                  this.parent.showFlag = true;
                  this.parent.addOrUpdateFlag = false;
                  this.parent.kechengpingjiaCrossAddOrUpdateFlag = false;
                  this.parent.search();
                  this.parent.contentStyleChange();
                }
              });
            } else {
              this.$message.error(data.msg);
            }
          });
        }
      });
    },
    // 获取uuid
    getUUID () {
      return new Date().getTime();
    },
    // 返回
    back() {
      this.parent.showFlag = true;
      this.parent.addOrUpdateFlag = false;
      this.parent.kechengpingjiaCrossAddOrUpdateFlag = false;
      this.parent.contentStyleChange();
    },
    kechengtupianUploadChange(fileUrls) {
	this.ruleForm.kechengtupian = fileUrls;
			this.addEditUploadStyleChange()
    },
	addEditStyleChange() {
	  this.$nextTick(()=>{
	    // input
	    document.querySelectorAll('.addEdit-block .input .el-input__inner').forEach(el=>{
	      el.style.height = this.addEditForm.inputHeight
	      el.style.color = this.addEditForm.inputFontColor
	      el.style.fontSize = this.addEditForm.inputFontSize
	      el.style.borderWidth = this.addEditForm.inputBorderWidth
	      el.style.borderStyle = this.addEditForm.inputBorderStyle
	      el.style.borderColor = this.addEditForm.inputBorderColor
	      el.style.borderRadius = this.addEditForm.inputBorderRadius
	      el.style.backgroundColor = this.addEditForm.inputBgColor
	    })
	    document.querySelectorAll('.addEdit-block .input .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.inputHeight
	      el.style.color = this.addEditForm.inputLableColor
	      el.style.fontSize = this.addEditForm.inputLableFontSize
	    })
	    // select
	    document.querySelectorAll('.addEdit-block .select .el-input__inner').forEach(el=>{
	      el.style.height = this.addEditForm.selectHeight
	      el.style.color = this.addEditForm.selectFontColor
	      el.style.fontSize = this.addEditForm.selectFontSize
	      el.style.borderWidth = this.addEditForm.selectBorderWidth
	      el.style.borderStyle = this.addEditForm.selectBorderStyle
	      el.style.borderColor = this.addEditForm.selectBorderColor
	      el.style.borderRadius = this.addEditForm.selectBorderRadius
	      el.style.backgroundColor = this.addEditForm.selectBgColor
	    })
	    document.querySelectorAll('.addEdit-block .select .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.selectHeight
	      el.style.color = this.addEditForm.selectLableColor
	      el.style.fontSize = this.addEditForm.selectLableFontSize
	    })
	    document.querySelectorAll('.addEdit-block .select .el-select__caret').forEach(el=>{
	      el.style.color = this.addEditForm.selectIconFontColor
	      el.style.fontSize = this.addEditForm.selectIconFontSize
	    })
	    // date
	    document.querySelectorAll('.addEdit-block .date .el-input__inner').forEach(el=>{
	      el.style.height = this.addEditForm.dateHeight
	      el.style.color = this.addEditForm.dateFontColor
	      el.style.fontSize = this.addEditForm.dateFontSize
	      el.style.borderWidth = this.addEditForm.dateBorderWidth
	      el.style.borderStyle = this.addEditForm.dateBorderStyle
	      el.style.borderColor = this.addEditForm.dateBorderColor
	      el.style.borderRadius = this.addEditForm.dateBorderRadius
	      el.style.backgroundColor = this.addEditForm.dateBgColor
	    })
	    document.querySelectorAll('.addEdit-block .date .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.dateHeight
	      el.style.color = this.addEditForm.dateLableColor
	      el.style.fontSize = this.addEditForm.dateLableFontSize
	    })
	    document.querySelectorAll('.addEdit-block .date .el-input__icon').forEach(el=>{
	      el.style.color = this.addEditForm.dateIconFontColor
	      el.style.fontSize = this.addEditForm.dateIconFontSize
	      el.style.lineHeight = this.addEditForm.dateHeight
	    })
	    // upload
	    let iconLineHeight = parseInt(this.addEditForm.uploadHeight) - parseInt(this.addEditForm.uploadBorderWidth) * 2 + 'px'
	    document.querySelectorAll('.addEdit-block .upload .el-upload--picture-card').forEach(el=>{
	      el.style.width = this.addEditForm.uploadHeight
	      el.style.height = this.addEditForm.uploadHeight
	      el.style.borderWidth = this.addEditForm.uploadBorderWidth
	      el.style.borderStyle = this.addEditForm.uploadBorderStyle
	      el.style.borderColor = this.addEditForm.uploadBorderColor
	      el.style.borderRadius = this.addEditForm.uploadBorderRadius
	      el.style.backgroundColor = this.addEditForm.uploadBgColor
	    })
	    document.querySelectorAll('.addEdit-block .upload .el-form-item__label').forEach(el=>{
	      el.style.lineHeight = this.addEditForm.uploadHeight
	      el.style.color = this.addEditForm.uploadLableColor
	      el.style.fontSize = this.addEditForm.uploadLableFontSize
	    })
	    document.querySelectorAll('.addEdit-block .upload .el-icon-plus').forEach(el=>{
	      el.style.color = this.addEditForm.uploadIconFontColor
	      el.style.fontSize = this.addEditForm.uploadIconFontSize
	      el.style.lineHeight = iconLineHeight
	      el.style.display = 'block'
	    })
	    // 多文本输入框
	    document.querySelectorAll('.addEdit-block .textarea .el-textarea__inner').forEach(el=>{
	      el.style.height = this.addEditForm.textareaHeight
	      el.style.color = this.addEditForm.textareaFontColor
	      el.style.fontSize = this.addEditForm.textareaFontSize
	      el.style.borderWidth = this.addEditForm.textareaBorderWidth
	      el.style.borderStyle = this.addEditForm.textareaBorderStyle
	      el.style.borderColor = this.addEditForm.textareaBorderColor
	      el.style.borderRadius = this.addEditForm.textareaBorderRadius
	      el.style.backgroundColor = this.addEditForm.textareaBgColor
	    })
	    document.querySelectorAll('.addEdit-block .textarea .el-form-item__label').forEach(el=>{
	      // el.style.lineHeight = this.addEditForm.textareaHeight
	      el.style.color = this.addEditForm.textareaLableColor
	      el.style.fontSize = this.addEditForm.textareaLableFontSize
	    })
	    // 保存
	    document.querySelectorAll('.addEdit-block .btn .btn-success').forEach(el=>{
	      el.style.width = this.addEditForm.btnSaveWidth
	      el.style.height = this.addEditForm.btnSaveHeight
	      el.style.color = this.addEditForm.btnSaveFontColor
	      el.style.fontSize = this.addEditForm.btnSaveFontSize
	      el.style.borderWidth = this.addEditForm.btnSaveBorderWidth
	      el.style.borderStyle = this.addEditForm.btnSaveBorderStyle
	      el.style.borderColor = this.addEditForm.btnSaveBorderColor
	      el.style.borderRadius = this.addEditForm.btnSaveBorderRadius
	      el.style.backgroundColor = this.addEditForm.btnSaveBgColor
	    })
	    // 返回
	    document.querySelectorAll('.addEdit-block .btn .btn-close').forEach(el=>{
	      el.style.width = this.addEditForm.btnCancelWidth
	      el.style.height = this.addEditForm.btnCancelHeight
	      el.style.color = this.addEditForm.btnCancelFontColor
	      el.style.fontSize = this.addEditForm.btnCancelFontSize
	      el.style.borderWidth = this.addEditForm.btnCancelBorderWidth
	      el.style.borderStyle = this.addEditForm.btnCancelBorderStyle
	      el.style.borderColor = this.addEditForm.btnCancelBorderColor
	      el.style.borderRadius = this.addEditForm.btnCancelBorderRadius
	      el.style.backgroundColor = this.addEditForm.btnCancelBgColor
	    })
	  })
	},
	addEditUploadStyleChange() {
		this.$nextTick(()=>{
		  document.querySelectorAll('.addEdit-block .upload .el-upload-list--picture-card .el-upload-list__item').forEach(el=>{
			el.style.width = this.addEditForm.uploadHeight
			el.style.height = this.addEditForm.uploadHeight
			el.style.borderWidth = this.addEditForm.uploadBorderWidth
			el.style.borderStyle = this.addEditForm.uploadBorderStyle
			el.style.borderColor = this.addEditForm.uploadBorderColor
			el.style.borderRadius = this.addEditForm.uploadBorderRadius
			el.style.backgroundColor = this.addEditForm.uploadBgColor
		  })
	  })
	},
  }
};
</script>
<style lang="scss">
.editor{
  height: 500px;
  
  & /deep/ .ql-container {
	  height: 310px;
  }
}
.amap-wrapper {
  width: 100%;
  height: 500px;
}
.search-box {
  position: absolute;
}
.addEdit-block {
	margin: -10px;
}
.detail-form-content {
	padding: 12px;
}
.btn .el-button {
  padding: 0;
}
</style>
