<style lang="less"></style>
<template>
  <div style="padding: 15px;">
    <Form
      v-width="400"
      mode="block"
      ref="form"
      :validOnChange="true"
      :showErrorTip="true"
      :labelWidth="110"
      :rules="rules"
      :model="record"
    >
      <FormItem label="变动金额" prop="credit1">
        <template v-slot:label>变动金额</template>
        <input type="number" v-model="record.credit1" />
      </FormItem>
      <FormItem label="变动说明" prop="remark">
        <template v-slot:label>变动说明</template>
        <input type="text" v-model="record.remark" />
      </FormItem>
      <FormItem>
        <Button color="primary" @click="create">保存</Button>
      </FormItem>
    </Form>
  </div>
</template>
<script>
export default {
  props: ['id'],
  data() {
    return {
      record: {
        credit1: 0,
        remark: null
      },
      rules: {
        required: ['credit1', 'remark']
      }
    };
  },
  methods: {
    create() {
      let validResult = this.$refs.form.valid();
      if (validResult.result) {
        let data = this.record;
        data.user_id = this.id;
        this.$emit('success', data);
      }
    }
  }
};
</script>
