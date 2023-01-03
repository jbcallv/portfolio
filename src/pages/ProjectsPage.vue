<template>
  <q-page padding>
    <q-table
      grid
      title="Projects"
      :rows="rows"
      :columns="columns"
      row-key="name"
      :filter="filter"
      hide-header
    >
      <template v-slot:item="props">
        <div class="q-pa-xs col-xs-12 col-sm-6 col-md-6">
          <q-card class="bg-dark">
            <q-card-section class="text-h6 text-weight-bold">
              {{ props.row.name }}
            </q-card-section>

            <q-card-section>
              <div class="text-body1">{{ props.row.description }}</div>
            </q-card-section>

            <q-card-section>
              <div class="row">
                <div class="text-body1 q-pr-md">
                  <q-icon name="code" />
                  {{ props.row.language }}
                </div>

                <div class="text-body1 q-pr-md">
                  <q-icon name="star" />
                  {{ props.row.stars }}
                </div>

                <div class="text-body1">
                  <q-icon name="fork_left" />
                  {{ props.row.forks }}
                </div>
              </div>
            </q-card-section>
          </q-card>
        </div>
      </template>
    </q-table>
  </q-page>
</template>

<script>
import { ref } from "vue";

const columns = [
  {
    name: "desc",
    required: true,
    align: "left",
    field: (row) => row.name,
    sortable: true,
  },
  {
    name: "description",
    align: "center",
    field: "calories",
    sortable: true,
  },
  {
    name: "language",
    align: "center",
    field: "language",
    sortable: true,
  },
  {
    name: "stars",
    align: "center",
    field: "stars",
    sortable: true,
  },
  {
    name: "forks",
    align: "center",
    field: "forks",
    sortable: true,
  },
];

const rows = [
  {
    name: "repo1",
    description: "this is an example repo for nothing",
    language: "C++",
    stars: 5,
    forks: 3,
  },
  {
    name: "repo2",
    description: "this is another example repo for nothing",
    language: "python",
    stars: 3,
    forks: 2,
  },
];

export default {
  name: "ProjectsPage",

  setup() {
    const filter = ref("");

    return { columns, rows, filter };
  },
};
</script>
