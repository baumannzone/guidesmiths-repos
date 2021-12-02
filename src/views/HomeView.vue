<script setup>
import repos from '@/components/data.js'
// Fetch data from an API
// const response = await fetch('https://open-source-info-api.herokuapp.com/api/v1/orgs/guidesmiths/repos',
//   {
//     method: 'GET',
//     headers: {
//       'Access-Control-Allow-Origin': '*',
//       'Content-Type': 'application/json',
//       'Accept': 'application/json'
//     }
//   }
// )
// const repos = await response.json()

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

          <div class="bg-white shadow overflow-hidden sm:rounded-md">
            <ul role="list" class="divide-y divide-gray-200">
              <li v-for="repo in repos" :key="repo.name">
                <a :href="repo.url" class="block hover:bg-gray-50" :title="repo.url">
                  <div class="px-4 py-4 sm:px-6">
                    <div class="flex items-center justify-between">
                      <p class="font-medium text-indigo-600 truncate">{{ repo.name }}</p>
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

                    <p class="leading-5 text-gray-500 truncate">{{ repo.description }}</p>
                    <div class="mt-2 sm:flex sm:justify-between">
                      <div class="sm:flex">
                        <p class="mt-2 flex items-center text-sm text-gray-500 sm:mt-0 sm:mr-4">
                          <!-- class="flex-shrink-0 mr-1.5 h-5 w-5 text-gray-400" -->
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
                          class="flex-shrink-0 mr-1.5 h-5 w-5 text-gray-400"
                          xmlns="http://www.w3.org/2000/svg"
                          viewBox="0 0 20 20"
                          fill="currentColor"
                          aria-hidden="true"
                        >
                          <path
                            fill-rule="evenodd"
                            d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z"
                            clip-rule="evenodd"
                          />
                        </svg>
                        <p>
                          Updated at
                          <time :datetime="repo.updatedAt">{{ repo.updatedAt }}</time>
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
