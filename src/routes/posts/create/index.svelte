<script>
    //import axios
    import axios from 'axios';

    //import Goto navigation
    import { goto } from '$app/navigation';

    //define variable
    let files   = '' ;
    let title   = '';
    let content = '';
    let validation = {};

    //method "storePost"
    const storePost = ( async () => {

        //define formData
        const formData = new FormData();

        //append data to "formData"
        formData.append('image', files[0]);
        formData.append('title', title);
        formData.append('content', content);

        //send data to server
        await axios.post('http://localhost:8000/api/posts', formData)
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
        <form on:submit|preventDefault={storePost}>

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
                SIMPAN
            </button>
        </form>
    </div>
</div>