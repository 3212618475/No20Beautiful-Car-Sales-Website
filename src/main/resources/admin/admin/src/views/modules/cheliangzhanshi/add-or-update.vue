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
        <el-form-item class="input" v-if="type!='info'" label="车辆编号" prop="cheliangbianhao">
            <el-input v-model="ruleForm.cheliangbianhao" 
                placeholder="车辆编号" readonly></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" v-if="ruleForm.cheliangbianhao" label="车辆编号" prop="cheliangbianhao">
              <el-input v-model="ruleForm.cheliangbianhao" 
                placeholder="车辆编号" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="select" v-if="type!='info'"  label="车辆品牌" prop="cheliangpinpai">
          <el-select v-model="ruleForm.cheliangpinpai" placeholder="请选择车辆品牌">
            <el-option
                v-for="(item,index) in cheliangpinpaiOptions"
                v-bind:key="index"
                :label="item"
                :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="车辆品牌" prop="cheliangpinpai">
	      <el-input v-model="ruleForm.cheliangpinpai"
                placeholder="车辆品牌" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="select" v-if="type!='info'"  label="车辆型号" prop="cheliangxinghao">
          <el-select v-model="ruleForm.cheliangxinghao" placeholder="请选择车辆型号">
            <el-option
                v-for="(item,index) in cheliangxinghaoOptions"
                v-bind:key="index"
                :label="item"
                :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="车辆型号" prop="cheliangxinghao">
	      <el-input v-model="ruleForm.cheliangxinghao"
                placeholder="车辆型号" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="颜色" prop="yanse">
          <el-input v-model="ruleForm.yanse" 
              placeholder="颜色" clearable  :readonly="ro.yanse"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="颜色" prop="yanse">
              <el-input v-model="ruleForm.yanse" 
                placeholder="颜色" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="select" v-if="type!='info'"  label="换挡方式" prop="huandangfangshi">
          <el-select v-model="ruleForm.huandangfangshi" placeholder="请选择换挡方式">
            <el-option
                v-for="(item,index) in huandangfangshiOptions"
                v-bind:key="index"
                :label="item"
                :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="换挡方式" prop="huandangfangshi">
	      <el-input v-model="ruleForm.huandangfangshi"
                placeholder="换挡方式" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="24">  
        <el-form-item class="upload" v-if="type!='info' && !ro.cheliangzhaopian" label="车辆照片" prop="cheliangzhaopian">
          <file-upload
          tip="点击上传车辆照片"
          action="file/upload"
          :limit="3"
          :multiple="true"
          :fileUrls="ruleForm.cheliangzhaopian?ruleForm.cheliangzhaopian:''"
          @change="cheliangzhaopianUploadChange"
          ></file-upload>
        </el-form-item>
        <div v-else>
          <el-form-item v-if="ruleForm.cheliangzhaopian" label="车辆照片" prop="cheliangzhaopian">
            <img style="margin-right:20px;" v-bind:key="index" v-for="(item,index) in ruleForm.cheliangzhaopian.split(',')" :src="item" width="100" height="100">
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="排量" prop="pailiang">
          <el-input v-model="ruleForm.pailiang" 
              placeholder="排量" clearable  :readonly="ro.pailiang"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="排量" prop="pailiang">
              <el-input v-model="ruleForm.pailiang" 
                placeholder="排量" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="车身类型" prop="cheshenleixing">
          <el-input v-model="ruleForm.cheshenleixing" 
              placeholder="车身类型" clearable  :readonly="ro.cheshenleixing"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="车身类型" prop="cheshenleixing">
              <el-input v-model="ruleForm.cheshenleixing" 
                placeholder="车身类型" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="车重" prop="chezhong">
          <el-input v-model="ruleForm.chezhong" 
              placeholder="车重" clearable  :readonly="ro.chezhong"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="车重" prop="chezhong">
              <el-input v-model="ruleForm.chezhong" 
                placeholder="车重" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="油箱容积" prop="youxiangrongji">
          <el-input v-model="ruleForm.youxiangrongji" 
              placeholder="油箱容积" clearable  :readonly="ro.youxiangrongji"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="油箱容积" prop="youxiangrongji">
              <el-input v-model="ruleForm.youxiangrongji" 
                placeholder="油箱容积" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="车门数" prop="chemenshu">
          <el-input v-model="ruleForm.chemenshu" 
              placeholder="车门数" clearable  :readonly="ro.chemenshu"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="车门数" prop="chemenshu">
              <el-input v-model="ruleForm.chemenshu" 
                placeholder="车门数" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="轴距" prop="zhouju">
          <el-input v-model="ruleForm.zhouju" 
              placeholder="轴距" clearable  :readonly="ro.zhouju"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="轴距" prop="zhouju">
              <el-input v-model="ruleForm.zhouju" 
                placeholder="轴距" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="车座" prop="chezuo">
          <el-input v-model="ruleForm.chezuo" 
              placeholder="车座" clearable  :readonly="ro.chezuo"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="车座" prop="chezuo">
              <el-input v-model="ruleForm.chezuo" 
                placeholder="车座" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="date" v-if="type!='info'" label="登记日期" prop="dengjiriqi">
            <el-date-picker
                format="yyyy 年 MM 月 dd 日"
                value-format="yyyy-MM-dd"
                v-model="ruleForm.dengjiriqi" 
                type="date"
                placeholder="登记日期">
            </el-date-picker> 
        </el-form-item>
        <div v-else>
          <el-form-item class="input" v-if="ruleForm.dengjiriqi" label="登记日期" prop="dengjiriqi">
              <el-input v-model="ruleForm.dengjiriqi" 
                placeholder="登记日期" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      <el-col :span="12">
        <el-form-item class="input" v-if="type!='info'"  label="价格" prop="price">
          <el-input v-model="ruleForm.price" 
              placeholder="价格" clearable  :readonly="ro.price"></el-input>
        </el-form-item>
        <div v-else>
          <el-form-item class="input" label="价格" prop="price">
              <el-input v-model="ruleForm.price" 
                placeholder="价格" readonly></el-input>
          </el-form-item>
        </div>
      </el-col>
      </el-row>
          <el-row>
            <el-col :span="24">
              <el-form-item v-if="type!='info'"  label="车辆详情" prop="cheliangxiangqing">
                <editor 
                    style="min-width: 200px; max-width: 600px;"
                    v-model="ruleForm.cheliangxiangqing" 
                    class="editor" 
                    action="file/upload">
                </editor>
              </el-form-item>
              <div v-else>
                <el-form-item v-if="ruleForm.cheliangxiangqing" label="车辆详情" prop="cheliangxiangqing">
                    <span v-html="ruleForm.cheliangxiangqing"></span>
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
	  addEditForm: {"btnSaveFontColor":"#fff","selectFontSize":"14px","btnCancelBorderColor":"#DCDFE6","inputBorderRadius":"4px","inputFontSize":"14px","textareaBgColor":"#fff","btnSaveFontSize":"14px","textareaBorderRadius":"4px","uploadBgColor":"#fff","textareaBorderStyle":"solid","btnCancelWidth":"88px","textareaHeight":"120px","dateBgColor":"#fff","btnSaveBorderRadius":"20px","uploadLableFontSize":"14px","textareaBorderWidth":"1px","inputLableColor":"#606266","addEditBoxColor":"#fff","dateIconFontSize":"14px","btnSaveBgColor":"rgba(251, 0, 29, 0.73)","uploadIconFontColor":"#8c939d","textareaBorderColor":"#DCDFE6","btnCancelBgColor":"#ecf5ff","selectLableColor":"#606266","btnSaveBorderStyle":"solid","dateBorderWidth":"1px","dateLableFontSize":"14px","dateBorderRadius":"4px","btnCancelBorderStyle":"solid","selectLableFontSize":"14px","selectBorderStyle":"solid","selectIconFontColor":"#C0C4CC","btnCancelHeight":"44px","inputHeight":"40px","btnCancelFontColor":"#606266","dateBorderColor":"#DCDFE6","dateIconFontColor":"#C0C4CC","uploadBorderStyle":"solid","dateBorderStyle":"solid","dateLableColor":"#606266","dateFontSize":"14px","inputBorderWidth":"1px","uploadIconFontSize":"28px","selectHeight":"40px","inputFontColor":"#606266","uploadHeight":"148px","textareaLableColor":"#606266","textareaLableFontSize":"14px","btnCancelFontSize":"14px","inputBorderStyle":"solid","btnCancelBorderRadius":"20px","inputBgColor":"#fff","inputLableFontSize":"14px","uploadLableColor":"#606266","uploadBorderRadius":"4px","btnSaveHeight":"44px","selectBgColor":"#fff","btnSaveWidth":"88px","selectIconFontSize":"14px","dateHeight":"40px","selectBorderColor":"#DCDFE6","inputBorderColor":"#DCDFE6","uploadBorderColor":"#DCDFE6","textareaFontColor":"#606266","selectBorderWidth":"1px","dateFontColor":"#606266","btnCancelBorderWidth":"1px","uploadBorderWidth":"1px","textareaFontSize":"14px","selectBorderRadius":"4px","selectFontColor":"#606266","btnSaveBorderColor":"rgba(251, 0, 29, 0.73)","btnSaveBorderWidth":"1px"},
      id: '',
      type: '',
      ro:{
	cheliangbianhao : false,
	cheliangpinpai : false,
	cheliangxinghao : false,
	yanse : false,
	huandangfangshi : false,
	cheliangzhaopian : false,
	pailiang : false,
	cheshenleixing : false,
	chezhong : false,
	youxiangrongji : false,
	chemenshu : false,
	zhouju : false,
	chezuo : false,
	dengjiriqi : false,
	cheliangxiangqing : false,
	clicktime : false,
	clicknum : false,
	price : false,
      },
      ruleForm: {
        cheliangbianhao: this.getUUID(),
        cheliangpinpai: '',
        cheliangxinghao: '',
        yanse: '',
        huandangfangshi: '',
        cheliangzhaopian: '',
        pailiang: '',
        cheshenleixing: '',
        chezhong: '',
        youxiangrongji: '',
        chemenshu: '',
        zhouju: '',
        chezuo: '',
        dengjiriqi: '',
        cheliangxiangqing: '',
        clicktime: '',
        price: '',
      },
          cheliangpinpaiOptions: [],
          cheliangxinghaoOptions: [],
          huandangfangshiOptions: [],
      rules: {
          cheliangbianhao: [
          ],
          cheliangpinpai: [
          ],
          cheliangxinghao: [
          ],
          yanse: [
          ],
          huandangfangshi: [
          ],
          cheliangzhaopian: [
          ],
          pailiang: [
          ],
          cheshenleixing: [
          ],
          chezhong: [
          ],
          youxiangrongji: [
          ],
          chemenshu: [
          ],
          zhouju: [
          ],
          chezuo: [
          ],
          dengjiriqi: [
          ],
          cheliangxiangqing: [
          ],
          clicktime: [
          ],
          clicknum: [
                { validator: validateIntNumber, trigger: 'blur' },
          ],
          price: [
                { required: true, message: '价格不能为空', trigger: 'blur' },
                { validator: validateNumber, trigger: 'blur' },
          ],
      }
    };
  },
  props: ["parent"],
  computed: {
  },
  created() {
	this.ruleForm.dengjiriqi = this.getCurDate()
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
          if(o=='cheliangbianhao'){
            this.ruleForm.cheliangbianhao = obj[o];
	    this.ro.cheliangbianhao = true;
            continue;
          }
          if(o=='cheliangpinpai'){
            this.ruleForm.cheliangpinpai = obj[o];
	    this.ro.cheliangpinpai = true;
            continue;
          }
          if(o=='cheliangxinghao'){
            this.ruleForm.cheliangxinghao = obj[o];
	    this.ro.cheliangxinghao = true;
            continue;
          }
          if(o=='yanse'){
            this.ruleForm.yanse = obj[o];
	    this.ro.yanse = true;
            continue;
          }
          if(o=='huandangfangshi'){
            this.ruleForm.huandangfangshi = obj[o];
	    this.ro.huandangfangshi = true;
            continue;
          }
          if(o=='cheliangzhaopian'){
            this.ruleForm.cheliangzhaopian = obj[o];
	    this.ro.cheliangzhaopian = true;
            continue;
          }
          if(o=='pailiang'){
            this.ruleForm.pailiang = obj[o];
	    this.ro.pailiang = true;
            continue;
          }
          if(o=='cheshenleixing'){
            this.ruleForm.cheshenleixing = obj[o];
	    this.ro.cheshenleixing = true;
            continue;
          }
          if(o=='chezhong'){
            this.ruleForm.chezhong = obj[o];
	    this.ro.chezhong = true;
            continue;
          }
          if(o=='youxiangrongji'){
            this.ruleForm.youxiangrongji = obj[o];
	    this.ro.youxiangrongji = true;
            continue;
          }
          if(o=='chemenshu'){
            this.ruleForm.chemenshu = obj[o];
	    this.ro.chemenshu = true;
            continue;
          }
          if(o=='zhouju'){
            this.ruleForm.zhouju = obj[o];
	    this.ro.zhouju = true;
            continue;
          }
          if(o=='chezuo'){
            this.ruleForm.chezuo = obj[o];
	    this.ro.chezuo = true;
            continue;
          }
          if(o=='dengjiriqi'){
            this.ruleForm.dengjiriqi = obj[o];
	    this.ro.dengjiriqi = true;
            continue;
          }
          if(o=='cheliangxiangqing'){
            this.ruleForm.cheliangxiangqing = obj[o];
	    this.ro.cheliangxiangqing = true;
            continue;
          }
          if(o=='clicktime'){
            this.ruleForm.clicktime = obj[o];
	    this.ro.clicktime = true;
            continue;
          }
          if(o=='clicknum'){
            this.ruleForm.clicknum = obj[o];
	    this.ro.clicknum = true;
            continue;
          }
          if(o=='price'){
            this.ruleForm.price = obj[o];
	    this.ro.price = true;
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
        } else {
          this.$message.error(data.msg);
        }
      });
            this.$http({
              url: `option/cheliangpinpai/cheliangpinpai`,
              method: "get"
            }).then(({ data }) => {
              if (data && data.code === 0) {
                this.cheliangpinpaiOptions = data.data;
              } else {
                this.$message.error(data.msg);
              }
            });
         
            this.$http({
              url: `option/cheliangxinghao/cheliangxinghao`,
              method: "get"
            }).then(({ data }) => {
              if (data && data.code === 0) {
                this.cheliangxinghaoOptions = data.data;
              } else {
                this.$message.error(data.msg);
              }
            });
         
            this.huandangfangshiOptions = "手动挡,自动挡".split(',')
    },
    // 多级联动参数
    info(id) {
      this.$http({
        url: `cheliangzhanshi/info/${id}`,
        method: "get"
      }).then(({ data }) => {
        if (data && data.code === 0) {
        this.ruleForm = data.data;
	//解决前台上传图片后台不显示的问题
	let reg=new RegExp('../../../upload','g')//g代表全部
	this.ruleForm.cheliangxiangqing = this.ruleForm.cheliangxiangqing.replace(reg,'../../../springbootil05r/upload');
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
            url: `cheliangzhanshi/${!this.ruleForm.id ? "save" : "update"}`,
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
                  this.parent.cheliangzhanshiCrossAddOrUpdateFlag = false;
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
      this.parent.cheliangzhanshiCrossAddOrUpdateFlag = false;
      this.parent.contentStyleChange();
    },
    cheliangzhaopianUploadChange(fileUrls) {
	this.ruleForm.cheliangzhaopian = fileUrls;
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
