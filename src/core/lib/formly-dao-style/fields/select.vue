<template>
  <field-item :to="to">
    <dao-select
      v-model="model[field.key]"
      :disabled="to.disabled"
      placeholder="请选择"
      no-data-text="没有符合条件的数据"
      :append-to-body="false">
      <dao-option-group>
        <dao-option
          v-for="item in to.options"
          :value="item.value"
          :label="item.label"
          :key="item.key">
        </dao-option>
      </dao-option-group>
    </dao-select>
  </field-item>
</template>

<script>
import baseField from './baseField';
import FieldItem from '../components/field-item';

export default {
  components: {
    FieldItem,
  },

  mixins: [baseField],

  created() {
    const model = this.getModel();
    if (model === undefined || model === null) {
      const { options = [] } = this.to;
      const firstOption = options[0] || {};
      this.onChange(firstOption.value);
      this.setModel(firstOption.value);
    }
  },

  methods: {
    onChange(e) {
      this.$set(this.form[this.field.key], '$dirty', true);
      this.runFunction('onChange', e);
    },
  },
};
</script>
