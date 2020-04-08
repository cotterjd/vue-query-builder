<template>
  <div class="q-card q-card--flat no-shadow q-pa-sm q-mb-md">
    <div class="row justify-between items-center no-wrap">
      <div class="col-auto q-ma-sm">{{ rule.label }}</div>

      <div class="row q-gutter-x-sm items-center no-wrap">
        <!-- List of operands (optional) -->
        <q-select
          v-if="typeof rule.operands !== 'undefined'"
          v-model="query.operand"
          v-bind="pSelect"
          :options="rule.operands"
          :clearable="false"
        />

        <!-- List of operators (e.g. =, !=, >, <) -->
        <q-select
          v-if="typeof rule.operators !== 'undefined' && rule.operators.length > 1"
          v-model="query.operator"
          v-bind="pSelect"
          :options="rule.operators"
          :clearable="false"
        />

        <!-- Basic text input -->
        <q-input
          v-if="rule.inputType === 'text'"
          v-model="query.value"
          v-bind="pInput"
          type="text"
          :placeholder="rule.placeholder"
        />

        <!-- Basic number input -->
        <q-input
          v-if="rule.inputType === 'number'"
          v-model="query.value"
          v-bind="pInput"
          type="number"
        />

        <!-- Datepicker -->
        <q-input
          v-if="rule.inputType === 'date'"
          v-model="query.value"
          v-bind="pInput"
          type="date"
        />

        <!-- Custom component input -->
        <div v-if="isCustomComponent" class="vqb-custom-component-wrap">
          <component :is="rule.component" :value="query.value" @input="updateQuery" />
        </div>

        <!-- Checkbox input -->
        <template v-if="rule.inputType === 'checkbox'">
          <q-option-group v-model="query.value" :options="rule.choices" type="checkbox" />
        </template>

        <!-- Radio input -->
        <template v-if="rule.inputType === 'radio'">
          <q-option-group v-model="query.value" :options="rule.choices" />
        </template>

        <!-- Select without groups -->
        <q-select
          v-if="rule.inputType === 'select' && !hasOptionGroups"
          v-model="query.value"
          :clearable="false"
          v-bind="pSelect"
          :multiple="rule.type === 'multi-select'"
          :options="selectOptions"
        />

        <!-- Select with groups -->
        <select
          v-if="rule.inputType === 'select' && hasOptionGroups"
          v-model="query.value"
          :multiple="rule.type === 'multi-select'"
        >
          <optgroup
            v-for="(option, option_key) in selectOptions"
            :key="option_key"
            :label="option_key"
          >
            <option
              v-for="sub_option in option"
              :key="sub_option.value"
              :value="sub_option.value"
            >{{ sub_option.label }}</option>
          </optgroup>
        </select>

        <!-- Remove rule button -->
        <q-btn round unelevated size="sm" type="button" icon="mdi-close" @click="remove" />
      </div>
    </div>
  </div>
</template>

<script>
import QueryBuilderRule from "../../components/QueryBuilderRule";

export default {
  extends: QueryBuilderRule,

  data: () => ({
    pBtn: {
      unelevated: true,
      dense: true
    },
    pInput: {
      class: `text-body2`,
      clearIcon: `mdi-close`,
      clearable: true,
      color: `primary`,
      dense: true,
      filled: true,
      hideHint: true
    },
    pSelect: {
      class: `text-body2`,
      clearIcon: `mdi-close`,
      clearable: true,
      color: `primary`,
      dense: true,
      filled: true,
      optionsDense: true
    }
  })
};
</script>
