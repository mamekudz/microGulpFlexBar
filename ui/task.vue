<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-text-field v-model="modelValue.data.workspacePath" :label="$t('Task.UI.Workspace')" hide-details outlined
          class="mx-2" @change="Refresh"></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-select v-model="modelValue.data.taskId" :items="taskItems" item-title="label" item-value="id"
          :label="$t('Task.UI.Task')" :no-data-text="$t('Task.UI.NoTasks')" hide-details outlined
          class="mx-2"></v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="8">
        <v-select v-model="modelValue.data.mode" :items="modeItems" item-title="label" item-value="value"
          :label="$t('Task.UI.Mode')" hide-details outlined class="mx-2"></v-select>
      </v-col>
      <v-col cols="4">
        <v-btn variant="tonal" block class="mx-2" @click="Refresh">{{ $t('Task.UI.Refresh') }}</v-btn>
      </v-col>
    </v-row>
    <v-row v-if="status">
      <v-col cols="12">
        <div class="mx-2 text-caption">{{ status }}</div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Object,
      required: true,
    },
  },
  emits: ['update:modelValue'],
  data() {
    return {
      tasks: [],
      status: '',
    };
  },
  computed: {
    taskItems() {
      return this.tasks.map((task) => ({ id: task.id, label: task.label || task.displayName || task.name }));
    },
    modeItems() {
      return [
        { value: 'run', label: this.$t('Task.UI.ModeRun') },
        { value: 'watch', label: this.$t('Task.UI.ModeWatch') },
      ];
    },
  },
  methods: {
    async Refresh() {
      // The backend owns the session token; the page only ever sees the
      // task list and a readable status line.
      const payload = await this.$fd.sendToBackend({
        action: 'refresh',
        workspacePath: this.modelValue.data.workspacePath || '',
        data: this.modelValue.data,
      });
      this.tasks = payload?.tasks || [];
      this.status = payload?.session?.allowed === false
        ? (payload.licenseMessage || payload.session.message || '')
        : (payload?.session?.workspacePath || '');
    },
  },
  mounted() {
    if (!this.modelValue.data.mode) this.modelValue.data.mode = 'run';
    this.Refresh();
  },
};
</script>

<style scoped></style>
