<template>
  <q-page padding>
    <div class="row flex-center q-pb-md">
      <q-avatar size="150px">
        <q-img :src="githubAvatarUrl" />
      </q-avatar>
    </div>

    <div class="row flex-center q-pb-md">
      <q-btn
        no-caps
        label="@jbcallv"
        class="text-accent"
        @click="openURL('https://github.com/jbcallv')"
      />
    </div>

    <div class="row flex-center text-center q-pb-md text-body1">
      {{ githubProfileBio }}
    </div>

    <div class="row flex-center text-center q-pb-md text-body1">
      {{ githubFollowerCount }} followers
    </div>

    <q-table
      grid
      :rows="rows"
      :columns="columns"
      row-key="name"
      hide-header
      :rows-per-page-options="[10]"
    >
      <template v-slot:item="props">
        <div class="q-pa-xs col-xs-12 col-sm-6 col-md-6">
          <q-card
            v-ripple
            class="bg-dark cursor-pointer q-hoverable"
            @click="openURL(props.row.link)"
          >
            <div class="q-focus-helper"></div>
            <q-card-section class="text-h6 text-weight-bold">
              {{ props.row.name }}
            </q-card-section>

            <q-card-section>
              <div class="text-body1">{{ props.row.description }}</div>
            </q-card-section>

            <q-card-section>
              <div class="row">
                <div class="text-body1 q-pr-md">
                  <q-icon
                    name="fa-solid fa-code"
                    style="vertical-align: text-top"
                    class="q-pr-xs"
                  />
                  {{ props.row.language }}
                </div>

                <div class="text-body1 q-pr-md">
                  <q-icon
                    name="fa-solid fa-star"
                    style="vertical-align: text-top"
                    class="q-pr-xs"
                  />
                  {{ props.row.stars }}
                </div>

                <div class="text-body1">
                  <q-icon
                    name="fa-solid fa-code-branch"
                    style="vertical-align: text-top"
                    class="q-pr-xs"
                  />
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
import { openURL } from "quasar";
import { ref } from "vue";
import axios from "axios";

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
  {
    name: "link",
    align: "center",
    field: "link",
    sortable: false,
  },
];

export default {
  name: "ProjectsPage",

  setup() {
    const githubApiUrl = `https://api.github.com/users/${
      import.meta.env.VITE_GITHUB_USERNAME
    }`;

    const githubAvatarUrl = ref(null);
    const githubFollowerCount = ref(0);
    const githubProfileBio = ref("");

    const rows = ref([]);

    setGithubProfileData();
    setGithubRepositoryData();

    async function setGithubProfileData() {
      const response = await axios.get(githubApiUrl);

      githubAvatarUrl.value = response.data.avatar_url;
      githubFollowerCount.value = response.data.followers;
      githubProfileBio.value = response.data.bio;
    }

    async function setGithubRepositoryData() {
      const response = await axios.get(`${githubApiUrl}/repos`);

      const formattedRepositories = response.data.map((repository) => {
        return {
          name: repository.name,
          description: repository.description
            ? repository.description
            : "No description",
          language: repository.language ? repository.language : "md",
          stars: repository.stargazers_count,
          forks: repository.forks_count,
          link: repository.html_url,
        };
      });

      rows.value = formattedRepositories;
    }

    return {
      columns,
      rows,
      githubAvatarUrl,
      githubProfileBio,
      githubFollowerCount,
      openURL,
    };
  },
};
</script>
