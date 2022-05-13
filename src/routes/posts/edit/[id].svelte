<script>
    //import hook onMount
    import { onMount } from 'svelte';

    //page params
    import { page } from '$app/stores';

    //import Goto navigation
    import { goto } from '$app/navigation';

    //import axios
    import axios from 'axios';

    //define variable
    let files   = '' ;
    let title   = '';
    let content = '';
    let validation = {};

    //method fetchDataPost
    const fetchDataPost = async () => {

        //fetch data from Rest API
        await axios.get(`http://localhost:8000/api/posts/${$page.params.id}`)
        .then(response => {

            //assign response data to variable
            title = response.data.data.title;
            content = response.data.data.content;

        });
    }

    //run hook "onMount"
    onMount(async () => {

        //call method "fetchDataPost"
        fetchDataPost();
    })


    //method "updatePost"
    const updatePost = ( async () => {

        //define formData
        const formData = new FormData();

        //append data to "formData"
        formData.append('image', files[0]);
        formData.append('title', title);
        formData.append('content', content);
        formData.append('_method', 'PATCH');

        //send data to server
        await axios.post(`http://localhost:8000/api/posts/${$page.params.id}`, formData)
        .then(() => {

            //redirect
            goto("/posts");

        })
        .catch((error) => {

            //assign validation on variable
            validation = error.response.data
        })

    });
</script>

<div class="card border-0 rounded-3 shadow-sm">
    <div class="card-body">
        <form on:submit|preventDefault={updatePost}>

            <div class="form-group mb-3">
                <!-- svelte-ignore a11y-label-has-associated-control -->
                <label class="form-label fw-bold">Image</label>
                <input type="file" accept="image/png, image/jpeg" bind:files class="form-control"/>
            </div>
            {#if validation.image}
                <!-- svelte-ignore invalid-html-attribute -->
                <div class="alert alert-danger">
                    {validation.image}
                </div>
            {/if}
            

            <div class="form-group mb-3">
                <!-- svelte-ignore a11y-label-has-associated-control -->
                <label class="form-label fw-bold">TITLE</label>
                <input class="form-control" bind:value={title} type="text" placeholder="Masukkan Title" />
            </div>
            {#if validation.title}
                <!-- svelte-ignore invalid-html-attribute -->
                <div class="alert alert-danger">
                    {validation.title}
                </div>
            {/if}


            <div class="form-group mb-3">
                <!-- svelte-ignore a11y-label-has-associated-control -->
                <label class="form-label fw-bold">CONTENT</label>
                <textarea class="form-control" rows={3} placeholder="Masukkan Content" bind:value={content} />
            </div>
            {#if validation.content}
                <!-- svelte-ignore invalid-html-attribute -->
                <div class="alert alert-danger">
                    {validation.content}
                </div>
            {/if}


            <button class="btn btn-primary border-0 shadow-sm" type="submit">
                UPDATE
            </button>
        </form>
    </div>
</div>