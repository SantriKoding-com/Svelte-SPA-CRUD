<header>
    <!-- Fixed navbar -->
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
        <div class="container">
            <a sveltekit:prefetch href="/" class="navbar-brand fw-bold">LARAVEL + SVELTE KIT</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarCollapse"
                aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarCollapse">
                <ul class="navbar-nav me-auto mb-2 mb-md-0">
                    <li class="nav-item">
                        <a sveltekit:prefetch href="/" class="nav-link" aria-current="page">HOME</a>
                    </li>
                    <li class="nav-item">
                        <a sveltekit:prefetch href="/posts" class="nav-link">POSTS</a>
                    </li>
                </ul>
                <form class="d-flex">
                    <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
                    <button class="btn btn-success" type="submit">Search</button>
                </form>
            </div>
        </div>
    </nav>
</header>

<div class="container" style="margin-top: 80px">
    <div class="row">
        <div class="col-md-12">

            <!-- render content-->
            <slot></slot>
        </div>
    </div>
</div>