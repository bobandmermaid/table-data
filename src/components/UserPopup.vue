<template>
  <div>
    <div class='button-add'>
      <el-button
        class='button'
        @click='dialogVisible = true'
        type='info' round>
        Добавить
      </el-button>
    </div>
    <el-dialog
      title='Добавление пользователя'
      :visible.sync='dialogVisible'
      @closed="resetForm('ruleForm')"
      width='400px'
      style='text-align: start'>
      <el-form
        :rules="rules"
        :label-position='labelPosition'
        :model='ruleForm'
        ref="ruleForm"
        label-width='120px'>
        <el-form-item label='Имя' prop='name'>
          <el-input
            type='text'
            v-model='ruleForm.name'>
          </el-input>
        </el-form-item>
        <el-form-item label='Телефон' prop='phone'>
          <el-input
            type='phone'
            v-mask='"+7 (###) ### ## ##"'
            v-model='ruleForm.phone'
            placeholder='+7 (123) 456 78 90'>
          </el-input>
        </el-form-item>
        <el-form-item label='Начальник' prop='chief'>
          <el-select
            v-model='ruleForm.chiefId'
            placeholder='Выбор из списка'
            style='width: 100%'>
            <el-option
              v-for="(item, index) in tableData"
              :key="'userItem '+ index"
              :label="item.name"
              :value="item.id">
            </el-option>
          </el-select>
        </el-form-item>
          <el-button
            class='button'
            type='info'
            @click="submitForm('ruleForm')"
            round>
            Сохранить
          </el-button>
      </el-form>
    </el-dialog>
  </div>
</template>

<script>

export default {
  name: 'UserPopup',
  props: {
    tableData: {
      type: Array,
      default: () => {
      },
    },
  },
  data() {
    return {
      dialogVisible: false,
      labelPosition: 'left',
      ruleForm: {
        name: '',
        phone: '',
        chiefId: null
      },
      rules: {
        name: [
          { required: true, message: 'Имя не заполнено', trigger: 'blur' },
          { min: 2, max: 30, message: 'Должно быть от 2 до 30 символов', trigger: 'blur' }
        ],
        phone: [
          { required: true, message: 'Телефон не заполнен', trigger: 'blur' },
        ],
        // chief: [
        //   { required: true, message: 'Нужно сделать выбор', trigger: 'change' }
        // ],
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          this.$emit('addUser', this.ruleForm);
          this.dialogVisible = false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
}
</script>

<style scoped>
.button-add {
  padding-bottom: 25px;
  text-align: end;
}

.button {
  padding: 13px 40px;
}
</style>
