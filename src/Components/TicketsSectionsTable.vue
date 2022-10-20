<template>
  <Head :title="__('Tickets sections')" />
  <Card :hasHeader="true" :hasActions="true">
    <template v-slot:header>
      <strong>{{ __("Tickets sections") }}</strong>
    </template>
    <template v-slot:actions>
      <Link
        :href="route('backend.ticket-sections.create')"
        class="btn btn-sm btn-success"
        >{{ __("Add new") }}</Link
      >
    </template>
    <div class="m-5">
      <data-table
        ref="servicesTypesTableRef"
        :columns="columns"
        :route="route('backend.ticket-sections.getData')"
        @setAction="setAction"
      />
    </div>
  </Card>
</template>

<script>
import DataTable from "@/Plugins/DataTable/DataTable.vue";
export default {
  components: { DataTable },
  props: {
    columns: Array,
  },
  methods: {
    setAction(data) {
      if (data.action == "href") {
        this.$inertia.visit(data.route);
      } else if (data.action == "delete") {
        this.areYouShure().then(async (res) => {
          if (res.isConfirmed) {
            await this.$inertia.delete(
              route("backend.ticket-sections.destroy", data.data.id)
            );
            this.$inertia.visit(route("backend.ticket-sections.index"));
          }
        });
      }
    },
  },
};
</script>

<style>
</style>