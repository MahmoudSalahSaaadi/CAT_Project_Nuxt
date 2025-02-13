<script setup>
import { reactive, ref } from "vue";
import { object, string } from "yup";
import { useAuthStore } from "~/stores/auth";
import { useApiFetch } from "~/composables/useApiFetch";
import { useNotificationsStore } from "~/stores/notifications";
import BaseInput from "~/components/_Shared/Forms/BaseInput.vue";
import BaseSubmitButton from "~/components/_Shared/Forms/BaseSubmitButton.vue";

definePageMeta({
  layout: "auth",
  middleware: "guest",
});

const router = useRouter();
const store = useAuthStore();
const notification = useNotificationsStore();

const schema = object({
  email: string().required().max(80).email(),
  password: string().required().min(8).max(30),
});

const form = reactive({
  email: "",
  password: "",
  remember_me: 1,
});

const loading = ref(false);
const showPassword = ref(false);

function handleBuChange(country) {
  store.activeBu = country // ksa || EG
  location.reload()
}

async function onSubmit() {
  loading.value = true;
  store.$reset();

  try {
    const response = await fetch("https://dummyjson.com/auth/login", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        username: form.email, // Adjust if necessary
        password: form.password,
        expiresInMins: 30,
      }),
      credentials: "include",
    });

    const data = await response.json();
    loading.value = false;

    if (!response.ok) {
      throw new Error(data.message || "Login failed");
    }

    const token = useCookie("token");
    store.authenticated = true;
    token.value = store.token = data.token;
    store.user = data;

    notification.push("success", "You are now logged in!");
    await router.push("/");

  } catch (error) {
    loading.value = false;
    notification.push("error", error.message);
  }
}

</script>

<template>
  <div class="flex flex-col justify-center">
    <div class="">
      <h2 class="font-bold">
        <span class="text-5xl">Homecare</span>
        <span class="text-4xl block">Login</span>
      </h2>

      <client-only>
        <VeeForm v-slot="{ handleSubmit }" :validation-schema="schema" class="mt-6 lg:mt-10">
          <form class="" @submit="handleSubmit($event, onSubmit)">
            <div class="mt-3">
              <VeeField v-slot="{ field }" name="email">
                <BaseInput v-model="form.email" name="email" :field="field" placeholder="Enter Email" type="email" />
                <VeeErrorMessage as="span" class="text-red-500" name="email" />
              </VeeField>
            </div>

            <div class="mt-3">
              <VeeField v-slot="{ field }" name="password">
                <BaseInput v-model="form.password" name="password" placeholder="Enter Password"
                  :type="showPassword ? 'text' : 'password'" :field="field">
                  <template #icon>
                    <img :src="`/images/design/auth/${showPassword ? 'eye-slash' : 'eyeIcon'
                      }.svg`" alt="eyeIcon" class="cursor-pointer h-5" @click.prevent="showPassword = !showPassword" />
                  </template>
                </BaseInput>
              </VeeField>
              <VeeErrorMessage as="span" class="text-red-500" name="password" />
            </div>

            <BaseSubmitButton label="Login" :loading="loading" class="w-full mt-6" />
          </form>
        </VeeForm>
      </client-only>
    </div>
  </div>
</template>
