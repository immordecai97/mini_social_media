<script setup>
import { ref, onMounted } from 'vue';
import ContainerComp from '@components/ContainerComp.vue';
import { getUserFromDB } from '@services/auth';

const userLogged = ref(null);

onMounted(async () => {
        try {
                const user = await getUserFromDB()
                if (!user) {
                        userLogged.value = null;
                        return;
                }
                userLogged.value = user;
        } catch (error) {
                console.error('Error getting user account:', error);
        }
});

const perfilPhotoDefault = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJQAAACUCAMAAABC4vDmAAAAMFBMVEXk5ueutLeor7Lf4ePn6eqrsbW5vsHIzM7a3d60ur3BxsjR1NbN0dPX2tzr7O29wsX2DjRMAAADaUlEQVR4nO2bW3LkIAwADYi3be5/25iZZB4bxyDZgqkt+ivZn+0SQgahTNNgMBgMBoPBYDAYDAaDwWCaAGBSG/mn3i53AFQMxt8xdpm6ewE466XU4getpZlVVy9YjHgKPcRE6Ke1KclfRnct2UkLprATpWe05g5W4PzfShmZVHOneGh0D1ZjK5j/yKZ3lpZLCPZ46R7Bcu2sKuN0i1Uzp1gXpxvN8qpeSQjTyMkgAiV0aJFWMGOctnrVpLZXJ/k3DRYQAi5Q2wJGdqkFqZThXj98oHKouK2wGZVhzqra78s/oXK8VobgxF2rHMVpY+WUipSU2goo5/pBoqTUtn6cZ+OV5sScVLTV4y0Kjhgp4fmOVajT3TuMUshTyxPG8kmr5xnGmnBCiu8C8b9JMS7fRyY6vSQwSi0fWDwn9YmfGaBKBUap1dOctGU8JVC3H29LaCGePHnvWKT104lVCgIpUMwXd1JR4KxSGcr+Y917NwhFXTIrTYQ7coNeHjhsVnFnVGZFtTyZL6IPFM7Js/YRfgBcWWduAz2sEN082e55prrPwV+iXii89T3i1NKp8tWhzWsDzqpxnDKlO6AW7J3q38BymFjSdHlvP3pu12LuYHRjdUHuaWlhew5xgApe6Fex7RffLUoPrWmxRkipM1KKNLv+IzjfuBjnuOTv3GcYAawvQN8Rqvy/K7dEG5L5Po4ak4KdF9dpvAtWtdhkvL5l02ue538RPoWoYG0oBpOKQUh9WNJz3pvZqSYRg9VZL3bL017B8iFyxwsmZ2uFniFLC2MpBYh7024VWt4yVQpQ9jiLDr1kYGhaHw+71WiJdHGTaosSMpP2kOnKWwTMlWfyAvq63ic4T+2//ta66L4M9iqju1Y6Xx+Kk5N4q9NTJhDP7bl9rZOZZS/Lple2S8UJJ+IYQhEt6ImF7EShoJasq1P8DeIjBGecMoRYAbeT0Ohsh8Cy797AdmjpT9gItEEtIL4vTULiPoTEx0YsGpHslLlJGr5eqs3iZRCN2tTKSVTPMNGnDwjoVPcgQX1SJ1pVherE7AhJqq6t3Wzr3amq67hHqvPImtMxceiVjimn+koaWT5DTaq3zahMcf2A8ucC5yhXdfqEG51UWrx23+InvphSLb97PxQz3cv2FN++VQeKyzcYDAaDwaA9XxcLKh2A6JUdAAAAAElFTkSuQmCC"


// Propiedades computadas para manejar la visibilidad
// const hasDisplayName = computed(() => userLogged.value && userLogged.value.displayName);
// const hasPhotoURL = computed(() => userLogged.value && userLogged.value.photoURL);
// const hasBio = computed(() => userLogged.value && userLogged.value.bio);
</script>

<template>
        <ContainerComp class="flex-1 flex flex-col">
                <ContainerComp class="flex-1 flex flex-col gap-4">
                        <ContainerComp tag="h1" text="Mi cuenta" class="text-3xl font-bold text-center" />
                        <ContainerComp class="flex flex-col ">
                                <ContainerComp tag="figure" class="max-w-96">
                                        <img :src="userLogged?.photoURL || 'https://placehold.co/1600x900'"
                                                alt="User cover photo" class="w-full">
                                </ContainerComp>
                                <ContainerComp class="max-w-96 flex justify-between items-end mt-2">
                                        <figure class="w-20 h-20 ml-2 -mt-20">
                                                <img :src="userLogged?.photoURL || perfilPhotoDefault"
                                                        alt="User cover photo"
                                                        class="aspect-w-1 rounded-full border-4 border-black">
                                        </figure>
                                        <router-link to="/account/edit"
                                                class="px-4 py-2 border rounded-lg text-center">Editar
                                                perfil</router-link>
                                </ContainerComp>
                        </ContainerComp>
                        <ContainerComp class="max-w-96 flex flex-col gap-2 justify-center items-center">
                                <ContainerComp>
                                        <ContainerComp class="flex flex-col items-center">
                                                <ContainerComp tag="h2" :text="`#${userLogged?.uid}`"
                                                        class="text-gray-500 text-opacity-80 text-xs" />
                                                <ContainerComp tag="h2" :text="userLogged?.displayName"
                                                        class="font-bold text-base" />
                                        </ContainerComp>
                                        <ContainerComp tag="p" :text="`Mail: ${userLogged?.email}`"
                                                class="text-gray-600" />
                                        <ContainerComp tag="p" :text="`@${userLogged?.username}`"
                                                class="text-gray-600" />

                                </ContainerComp>
                                <ContainerComp tag="p" :text="userLogged?.bio" class="break-words whitespace-normal" />
                                <ContainerComp tag="p" text="Traer minitweets proximamente..." class="break-words whitespace-normal text-gray-400 text-center text-opacity-50 my-24" />
                        </ContainerComp>
                </ContainerComp>
        </ContainerComp>
</template>