<template>
  <div class="q-card q-card--flat no-shadow" :class="depth > 1 ? `q-ma-md q-card--bordered` : ``">
    <!-- <div class="q-card__section q-card__section--vert q-gutter-y-md"> -->
    <!-- <div class="row no-wrap justify-between"> -->
    <q-toolbar style="min-height: 40px" class="bg-blue-grey-1">
      <q-select
        v-model="selectedRule"
        v-bind="pSelect"
        :options="rules"
        :clearable="false"
      />

      <q-btn-group unelevated>
        <q-btn
          v-bind="pBtn"
          size="sm"
          :dense="false"
          class="text-primary"
          icon="mdi-plus"
          @click="addRule"
        />

        <q-btn
          v-if="depth < maxDepth"
          v-bind="pBtn"
          size="sm"
          :dense="false"
          class="text-primary"
          icon="mdi-expand-all-outline"
          @click="addGroup"
        />

        <q-select
          v-model="query.logicalOperator"
          :clearable="false"
          :options="labels.matchTypes"
          :filled="false"
          class="q-mx-sm text-body2"
          v-bind="pSelect"
        />

        <q-btn
          v-if="depth > 1"
          v-bind="pBtn"
          size="sm"
          :dense="false"
          class="text-primary"
          icon="mdi-close"
          @click="remove"
        />

        <!-- <q-btn-dropdown>
            <q-list padding>
              <q-item
                v-for="label in labels.matchTypes"
                :key="label.index"
                v-model="query.logicalOperator"
                clickable
              >
                {{ label.label }}
              </q-item>
            </q-list>
          </q-btn-dropdown> -->
      </q-btn-group>
      <!-- </div> -->
    </q-toolbar>

    <query-builder-children v-bind="$props" />
    <!-- </div> -->
  </div>
</template>

<script>
import { pBtn, pSelect, pInput } from '@/static/props'
import QueryBuilderGroup         from 'vue-query-builder/dist/group/QueryBuilderGroup.umd'
import QueryBuilderRule          from './o.query-builder.rule'

export default {
  name: `QueryBuilderGroup`,

  components: {
    // eslint-disable-next-line vue/no-unused-components
    QueryBuilderRule
  },

  extends: QueryBuilderGroup,

  data: () => ({
    pBtn,
    pInput,
    pSelect
  })
}
</script>
