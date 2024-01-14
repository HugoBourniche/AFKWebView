<script>
    import {Link} from "svelte-routing";
</script>

<nav class="navbar navbar-expand-lg navbar-light">
    <Link class="navbar-brand" to="/" >
        <img src="/resources/img/logo.png" width="80" class="d-inline-block align-top" alt="logo">
    </Link>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
            <li class="nav-item">
                <Link class="nav-link" to="/" >Personnages</Link>
            </li>
            <li class="nav-item">
                <Link class="nav-link" to="/team" >Team</Link>
            </li>
            <li class="nav-item">
                <Link class="nav-link" to="/tuto" >Tuto</Link>
            </li>
        </ul>
    </div>
</nav>

<style>
    .nav-link {
        cursor: pointer;
    }

    .navbar {
        background: rgb(255,255,255);
        background: linear-gradient(0deg, rgba(255,255,255,1) 0%, rgba(252,255,186,0.6890996011455408) 54%, rgba(161,125,14,0.475616455078125) 100%);
    }
</style>
