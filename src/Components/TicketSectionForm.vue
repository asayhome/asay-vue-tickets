<template>
  <Head :title="__('Ticket section data')" />
  <form @submit.prevent="store">
    <Card :hasHeader="true" :hasActions="true" :hasFooter="true">
      <template v-slot:header>
        <strong>{{ __("Ticket section data") }}</strong>
      </template>
      <template v-slot:actions>
        <Link
          :href="route('backend.ticket-sections.index')"
          class="btn btn-sm btn-danger"
          >{{ __("Back") }}</Link
        >
      </template>
      <div class="m-5">
        <div class="row">
          <div class="col-md-6">
            <Input
              id="name"
              type="text"
              :label="__('Name')"
              v-model="form.name"
              :errorMessage="form.errors.name"
              :action="action"
            />
          </div>
        </div>
      </div>
      <template v-slot:footer v-if="action != 'show'">
        <button
          class="btn btn-sm btn-success"
          @click="storeUserData"
          :disabled="form.processing"
        >
          {{ __("Save") }}
        </button>
      </template>
    </Card>
  </form>
</template>

<script>
import Input from "@/Components/Backend/Input.vue";
import BackendLayout from "@/Layouts/BackendLayout.vue";
import { useForm } from "@inertiajs/inertia-vue3";
import { ref } from "vue";
export default {
  layout: BackendLayout,
  components: {
    Input,
  },
  props: {
    action: String,
    ticketSection: Object,
  },
  setup(props) {
    let form = ref(
      useForm({
        action: props.action,
        id: props.ticketSection?.id,
        name: props.ticketSection?.name,
      })
    );
    return {
      form,
    };
  },
  methods: {
    store() {
      this.form.post(route("backend.ticket-sections.store"), {
        preserveScroll: true,
      });
    },
  },
};
</script>

<style>
</style>