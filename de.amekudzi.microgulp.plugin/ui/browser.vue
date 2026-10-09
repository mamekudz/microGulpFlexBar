<template>
	<div class="microgulp-browser-config">
		<div class="row">
			<label>{{ $t('Browser.UI.Workspace') }}</label>
			<input type="text" v-model="modelValue.workspacePath" :disabled="modelValue.followActive" />
		</div>
		<div class="row switch">
			<label>
				<input type="checkbox" v-model="modelValue.followActive" />
				{{ $t('Browser.UI.Follow') }}
			</label>
			<p class="hint">{{ $t('Browser.UI.FollowHint') }}</p>
		</div>
		<div class="row">
			<label>{{ $t('Browser.UI.Width') }}</label>
			<input type="number" min="120" max="1000" step="10" v-model.number="modelValue.width" />
		</div>
		<p class="hint">{{ $t('Browser.UI.Hint') }}</p>
	</div>
</template>

<script>
export default {
	name: 'MicroGulpBrowserConfig',
	props: {
		modelValue: {
			type: Object,
			required: true,
		},
	},
	mounted() {
		if (this.modelValue.width == null || this.modelValue.width === '') {
			this.modelValue.width = 480;
		}
		if (this.modelValue.followActive == null) {
			this.modelValue.followActive = false;
		}
		if (this.modelValue.workspacePath == null) {
			this.modelValue.workspacePath = '';
		}
	},
};
</script>

<style scoped>
.microgulp-browser-config { display: flex; flex-direction: column; gap: 12px; }
.row { display: flex; flex-direction: column; gap: 4px; }
.row.switch label { display: flex; align-items: center; gap: 8px; }
input[type="text"], input[type="number"] { width: 100%; }
.hint { opacity: 0.75; font-size: 12px; margin: 0; }
</style>
