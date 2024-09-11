<script lang="ts" setup>
import type { RouteParams } from 'vue-router';
import type { Database } from '~/database.types';

const params = useRoute().params
const client = useSupabaseClient<Database>()

if(!params.id) {
    throw createError({
        message: "Not found",
        statusCode: 404,
    })
}

const { data } = useAsyncData('link', async () => {
    const { data, error } = await client.from('links').select('*').eq('key', params.id).single()

    if(error) {
        throw createError({
            statusCode: 404,
            message: "Not found"
        })
    }

    return data
})

if(data.value?.long_url) {
    useExternalRedirect(data.value?.long_url)
}
</script>

<template>
    
</template>