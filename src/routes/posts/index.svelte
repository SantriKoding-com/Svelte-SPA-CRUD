<script>
    //import hook onMount
    import { onMount } from 'svelte';

    //import axios
    import axios from 'axios';

    //define variable
    let posts = [];

    //method "fetchDataPosts"
    const fetchDataPosts = async () => {
        
        //fetch data from Rest API
        await axios.get('http://localhost:8000/api/posts')
        .then(response => {

            //assign response data to variable posts
            posts = response.data.data.data
        })
    }

    //run hook "onMount"
    onMount(async () => {

        //call method "fetchDataPosts"
        fetchDataPosts();
    });

    //method "deletePost"
    const deletePost = async (id) => {

        await axios.delete(`http://localhost:8000/api/posts/${id}`)
        .then(() => {

            //call method "fetchDataPosts"
            fetchDataPosts();
        })

    };

</script>

<div class="card border-0 rounded-3 shadow-sm">
    <div class="card-body">
        <a sveltekit:prefetch href="/posts/create" class="btn btn-success btn-md shadow-sm rounded-3 border-0 mb-3">TAMBAH</a>
        <table class="table table-striped table-bordered mb-0">
            <thead>
                <tr>
                    <th scope="col">Image</th>
                    <th scope="col">Title</th>
                    <th scope="col">Content</th>
                    <th scope="col">Actions</th>
                </tr>
            </thead>
            <tbody>
                {#each posts as post}
                    <tr>
                        <td class="text-center">
                            <!-- svelte-ignore a11y-missing-attribute -->
                            <img src={`http://localhost:8000/storage/posts/${post.image}`} width="150" class="rounded-3"/>
                        </td>
                        <td>{ post.title }</td>
                        <td>{ post.content }</td>
                        <td class="text-center">
                            <a sveltekit:prefetch href={`/posts/edit/${post.id}`} class="btn btn-sm btn-primary border-0 shadow-sm mb-3">EDIT</a>
                            <button on:click={() => deletePost(post.id)} class="btn btn-sm btn-danger border-0 shadow-sm mb-3">DELETE</button>
                        </td>
                    </tr>
                {/each}
            </tbody>
        </table>
    </div>
</div>