<template>
  <div style="padding: 15px;">
    <Form
      v-width="400"
      mode="block"
      ref="form"
      :validOnChange="true"
      :showErrorTip="true"
      :rules="rules"
      :model="category"
    >
      <FormItem label="父级" prop="parent_id">
        <template v-slot:label>父级</template>
        <Select
          v-model="category.parent_id"
          :datas="categories"
          keyName="id"
          titleName="name"
          :filterable="true"
        ></Select>
      </FormItem>
      <FormItem label="分类名" prop="name">
        <template v-slot:label>分类名</template>
        <input type="text" v-model="category.name" />
      </FormItem>
      <FormItem label="排序" prop="sort">
        <template v-slot:label>排序</template>
        <input type="number" v-model="category.sort" />
      </FormItem>
      <FormItem>
        <Button color="primary" @click="create">添加</Button>
        <Button @click="cancel">取消</Button>
      </FormItem>
    </Form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      category: {
        name: '',
        sort: 0,
        parent_id: 0
      },
      categories: [],
      rules: {
        required: ['name', 'sort']
      }
    };
  },
  mounted() {
    R.Extentions.paper.QuestionCategory.Create().then(res => {
      this.categories = res.data.categories;
    });
  },
  methods: {
    create() {
      let validResult = this.$refs.form.valid();
      if (validResult.result) {
        this.$emit('success', this.category);
        this.close();
      }
    },
    cancel() {
      this.close();
    },
    close() {
      this.$emit('close');
    }
  }
};
</script>
