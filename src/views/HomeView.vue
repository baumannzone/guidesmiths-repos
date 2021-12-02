<script setup>
import { onMounted, ref } from 'vue'
import repos from '@/components/data.js'
// Fetch data from an API
// const response = await fetch('https://open-source-info-api.herokuapp.com/api/v1/orgs/guidesmiths/repos')
//   .then(response => response.json())

const searchText = ref('')
const filteredRepos = ref(repos)

const formatDate = date => {
  const d = new Date(date)
  return `${d.getMonth() + 1}/${d.getDate()}/${d.getFullYear()}`
}

const filterRepos = () => {
  const search = searchText.value.toLowerCase()
  filteredRepos.value = repos.filter(repo => {
    repo.description = repo.description || ''
    return repo.name.toLowerCase().includes(search) || repo.description.toLowerCase().includes(search)
  })
}

const onChange = () => {
  if (searchText.value.length > 0) {
    filterRepos()
  } else {
    filteredRepos.value = repos
  }
}


</script>

<template>
  <main>
    <div class="bg-white">
      <div class="mx-auto py-12 px-4 max-w-7xl sm:px-6 lg:px-8 lg:py-24">
        <div class="space-y-12">
          <div class="space-y-5 sm:space-y-4 md:max-w-xl lg:max-w-3xl xl:max-w-none">
            <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">Guidesmiths Repos</h2>
            <p class="text-xl text-gray-500">We are open source</p>
          </div>

          <div class="grid grid-cols-2 gap-4">
            <div>
              <div
                class="relative border border-gray-300 rounded-md px-3 py-2 shadow-sm focus-within:ring-1 focus-within:ring-pink-600 focus-within:border-pink-600"
              >
                <label
                  for="search"
                  class="absolute -top-2 left-2 -mt-px inline-block px-1 bg-white text-xs font-medium text-gray-900"
                >Search</label>
                <input
                  type="text"
                  name="search"
                  id="search"
                  v-model="searchText"
                  class="block w-full border-0 p-0 text-gray-900 placeholder-gray-500 focus:ring-0 sm:text-sm"
                  placeholder="Search by name"
                  @input="onChange"
                />
              </div>
            </div>
            <div class="flex items-center justify-end">
              <p class="text-gray-500 text-xl font-medium">Showing {{ filteredRepos.length }} repos</p>
            </div>
          </div>

          <div class="bg-white shadow overflow-hidden sm:rounded-md">
            <ul role="list" class="divide-y divide-gray-200">
              <li v-for="repo in filteredRepos" :key="repo.name">
                <a :href="repo.url" class="block hover:bg-gray-50">
                  <div class="px-4 py-4 sm:px-6">
                    <div class="flex items-center justify-between">
                      <p
                        class="font-medium text-xl text-pink-600 truncate"
                        :title="repo.url"
                      >{{ repo.name }}</p>
                      <div class="ml-2 flex-shrink-0 flex space-x-4">
                        <p
                          v-if="repo.hasIssues"
                          class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-pink-100 text-pink-800"
                        >Issues</p>
                        <p
                          v-if="repo.hasLinter"
                          class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-indigo-100 text-indigo-800"
                        >Linter</p>
                        <p
                          v-if="repo.hasTests"
                          class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800"
                        >Tests</p>
                      </div>
                    </div>

                    <div class="mt-2">
                      <p
                        class="leading-5 text-gray-500 truncate max-w-full sm:max-w-screen-sm"
                      >{{ repo.description }}</p>
                    </div>
                    <div class="mt-4 sm:flex sm:justify-between">
                      <div class="sm:flex">
                        <p
                          class="mt-2 flex items-center text-sm text-gray-500 sm:mt-0 sm:mr-4"
                          title="Size"
                        >
                          <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-6 w-6"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M7 7h.01M7 3h5c.512 0 1.024.195 1.414.586l7 7a2 2 0 010 2.828l-7 7a2 2 0 01-2.828 0l-7-7A1.994 1.994 0 013 12V7a4 4 0 014-4z"
                            />
                          </svg>
                          {{ repo.size }}
                        </p>
                        <p
                          class="flex items-center text-sm text-gray-500 mt-2 sm:mt-0"
                          v-if="repo.ci"
                          title="CI"
                        >
                          <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-6 w-6 mr-2"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              stroke-width="2"
                              d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                            />
                          </svg>
                          {{ repo.ci }}
                        </p>
                      </div>

                      <div class="flex items-center text-sm text-gray-500 sm:mt-0">
                        <!-- Heroicon name: solid/calendar -->
                        <svg
                          xmlns="http://www.w3.org/2000/svg"
                          class="flex-shrink-0 mr-1.5 h-5 w-5 text-gray-400"
                          fill="none"
                          viewBox="0 0 24 24"
                          stroke="currentColor"
                        >
                          <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                          />
                        </svg>
                        <p>
                          <time
                            :title="`Updated at ${formatDate(repo.updatedAt)}`"
                            :datetime="repo.updatedAt"
                          >{{ formatDate(repo.updatedAt) }}</time>
                        </p>
                      </div>
                    </div>
                  </div>
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
