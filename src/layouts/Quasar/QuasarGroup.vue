<template>
  <div class="q-card q-card--flat no-shadow" :class="depth > 1 ? `q-ma-md q-card--bordered` : ``">
    <q-toolbar style="min-height: 40px" class="bg-blue-grey-1">
      <q-select
        v-model="selectedRule"
        v-bind="pSelect"
        :options="rules"
        :clearable="false"
      >
        <q-tooltip>
          Choose field for search criteria.
        </q-tooltip>
      </q-select>

      <q-btn-group unelevated>
        <q-btn
          v-bind="pBtn"
          size="sm"
          :dense="false"
          class="text-primary"
          icon="mdi-plus"
          @click="addRule"
        >
          <q-tooltip>
            Add selected field to search criteria.
          </q-tooltip>
        </q-btn>

        <q-btn
          v-if="depth < maxDepth"
          v-bind="pBtn"
          size="sm"
          :dense="false"
          class="text-primary"
          icon="mdi-expand-all-outline"
          @click="addGroup"
        >
          <q-tooltip>
            Add nested criteria group.
          </q-tooltip>
        </q-btn>

        <q-select
          v-model="query.logicalOperator"
          :clearable="false"
          :options="labels.matchTypes"
          :filled="false"
          class="q-mx-sm text-body2"
          v-bind="pSelect"
        >
          <q-tooltip>
            Change logical operator.
          </q-tooltip>
        </q-select>

        <q-btn
          v-if="depth > 1"
          v-bind="pBtn"
          size="sm"
          :dense="false"
          class="text-primary"
          icon="mdi-close"
          @click="remove"
        />
          <q-tooltip>
            Remove nested criteria group.
          </q-tooltip>
        </q-btn>
      </q-btn-group>
    </q-toolbar>

    <query-builder-children v-bind="$props" />
  </div>
</template>

<script>
import QueryBuilderGroup from '../../components/QueryBuilderGroup'
import QueryBuilderRule  from './QuasarRule.vue'

export default {
  name: `QueryBuilderGroup`,

  components: {
    // eslint-disable-next-line vue/no-unused-components
    QueryBuilderRule
  },

  extends: QueryBuilderGroup,

  data: () => ({
    pBtn: {
      unelevated: true
    },
    pInput: {
      inputClass: `text-body2`,
      clearIcon:  `mdi-close`,
      clearable:  true,
      color:      `primary`,
      dense:      true,
      filled:     true,
      hideHint:   true,
    },
    pSelect: {
      inputClass:   `text-body2`,
      clearIcon:    `mdi-close`,
      clearable:    true,
      color:        `primary`,
      dense:        true,
      filled:       true,
      optionsDense: true,
    }
  })
}
</script>

