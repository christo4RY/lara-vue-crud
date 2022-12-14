<template>
  <div class="flex place-content-end mb-4">
    <div
      class="
        px-4
        py-2
        text-white
        bg-gray-800
        hover:bg-indigo-700
        cursor-pointer
        rounded-md
      "
    >
      <router-link :to="{ name: 'client.create' }" class="text-sm font-medium"
        >Create Client</router-link
      >
    </div>
  </div>
  <div
    class="
      overflow-hidden overflow-x-auto
      min-w-full
      align-middle
      sm:rounded-md
    "
  >
    <table class="min-w-full border divide-y divide-gray-200">
      <thead>
        <tr>
          <th class="px-6 py-3 bg-gray-50">
            <span
              class="
                text-xs
                font-medium
                tracking-wider
                leading-4
                text-left text-gray-500
                uppercase
              "
              >Name</span
            >
          </th>
          <th class="px-6 py-3 bg-gray-50">
            <span
              class="
                text-xs
                font-medium
                tracking-wider
                leading-4
                text-left text-gray-500
                uppercase
              "
              >Email</span
            >
          </th>
          <th class="px-6 py-3 bg-gray-50">
            <span
              class="
                text-xs
                font-medium
                tracking-wider
                leading-4
                text-left text-gray-500
                uppercase
              "
              >Address</span
            >
          </th>
          <th class="px-6 py-3 bg-gray-50">
            <span
              class="
                text-xs
                font-medium
                tracking-wider
                leading-4
                text-left text-gray-500
                uppercase
              "
              >Website</span
            >
          </th>
          <th class="px-6 py-3 bg-gray-50">
            <span
              class="
                text-xs
                font-medium
                tracking-wider
                leading-4
                text-left text-gray-500
                uppercase
              "
              >Action</span
            >
          </th>
        </tr>
      </thead>

      <tbody class="bg-white divide-y divide-gray-200 divide-solid">
        <template v-for="client in clients" :key="client.id">
          <tr class="bg-white">
            <td
              class="
                px-6
                py-4
                text-sm
                leading-5
                text-gray-900
                whitespace-no-wrap
              "
            >
              {{ client.name }}
            </td>
            <td
              class="
                px-6
                py-4
                text-sm
                leading-5
                text-gray-900
                whitespace-no-wrap
              "
            >
              {{ client.email }}
            </td>
            <td
              class="
                px-6
                py-4
                text-sm
                leading-5
                text-gray-900
                whitespace-no-wrap
              "
            >
              {{ client.address }}
            </td>
            <td
              class="
                px-6
                py-4
                text-sm
                leading-5
                text-gray-900
                whitespace-no-wrap
              "
            >
              {{ client.website }}
            </td>
            <td
              class="
                px-6
                py-4
                text-sm text-center
                leading-5
                text-gray-900
                whitespace-no-wrap
              "
            >
              <router-link
                :to="{ name: 'client.edit', params: { id: client.id } }"
                class="
                  mr-2
                  inline-flex
                  items-center
                  px-4
                  py-2
                  bg-gray-800
                  border border-transparent
                  rounded-md
                  font-semibold
                  text-xs text-white
                  uppercase
                  tracking-widest
                  hover:bg-gray-700
                  active:bg-gray-900
                  focus:outline-none focus:border-gray-900 focus:ring
                  ring-gray-300
                  disabled:opacity-25
                  transition
                  ease-in-out
                  duration-150
                "
              >
                Edit</router-link
              >
              <button
                @click="deleteClient(client.id)"
                class="
                  inline-flex
                  items-center
                  px-4
                  py-2
                  bg-gray-800
                  border border-transparent
                  rounded-md
                  font-semibold
                  text-xs text-white
                  uppercase
                  tracking-widest
                  hover:bg-gray-700
                  active:bg-gray-900
                  focus:outline-none focus:border-gray-900 focus:ring
                  ring-gray-300
                  disabled:opacity-25
                  transition
                  ease-in-out
                  duration-150
                "
              >
                Delete
              </button>
            </td>
          </tr>
        </template>
      </tbody>
    </table>
  </div>
</template>

<script>
import useClient from "../../composables/clients";
import { onMounted } from "vue";
import Swal from "sweetalert2";

export default {
  setup() {
    const { clients, getClients, destroyClient } = useClient();
    const deleteClient = (id) => {
      //   if (!window.confirm("You sure?")) {
      //     return;
      //   }

      Swal.fire({
        title: "Are you sure?",
        text: "You won't be able to revert this!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Yes, delete it!",
      }).then((result) => {
        if (result.isConfirmed) {
          destroyClient(id);
          getClients();
          Swal.fire("Deleted!", "Your file has been deleted.", "success");
        }
      });
    };
    onMounted(getClients);
    return {
      clients,
      deleteClient,
    };
  },
};
</script>
