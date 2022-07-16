<template>
    <div>
        <nav class="navBar">

            <div class="containerTogglerBtn navbar-dark p-0">
                <button id="sidebarBtn" class="navbar-toggler" type="button" v-on:click.prevent="showHideSideMenu()">
                    <Transition name="menu">
                        <svg v-show="!showSideBar" xmlns="http://www.w3.org/2000/svg" fill="currentColor"
                            class="menuIn bi bi-list position-absolute" viewBox="0 0 16 16">
                            <path fill-rule="evenodd"
                                d="M2.5 12a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5z" />
                        </svg>
                    </Transition>

                    <Transition name="menu">
                        <svg v-show="showSideBar" xmlns="http://www.w3.org/2000/svg" width="16" height="16"
                            fill="currentColor" class="menuOut bi bi-x-lg position-absolute" viewBox="0 0 16 16">
                            <path
                                d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8 2.146 2.854Z" />
                        </svg>
                    </Transition>

                </button>
            </div>

            <form class="searchArea" role="search">
                <input class="form-control me-3" type="search" placeholder="Pesquisar" aria-label="Search">
                <button class="btn btn-outline-success" type="submit">Buscar</button>
            </form>

            <form class="searchAreaMobile" role="search">
                <input class="inputMobile form-control" type="search" placeholder="Pesquisar" aria-label="Search">
                <i class="btnSearchMobile bi bi-search"></i>
            </form>

        </nav>

        <div id="navSider" class="navSider" :class="sideInOut">
            <div class="userPicture" v-show="showSideBar">
                <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" class="bi bi-pencil-square editImg"
                    viewBox="0 0 16 16">
                    <path
                        d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z" />
                    <path fill-rule="evenodd"
                        d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z" />
                </svg>

                <img class="border border-white rounded-circle userImg" :src="userImage" v-on:click="chooseImage()" />
                <input class="form-control d-none" type="file" id="choosePic" accept="image/*"
                    v-on:input="injectNewPic()">
            </div>

            <p class="m-0 p-0" v-show="showSideBar">Admin</p>
            <hr class="m-1 mb-3" size="3" width="90%" v-show="showSideBar">

            <div class="expandSideBar d-flex row w-100" v-if="showSideBar">
                <a>Perfil</a>
                <a>Biografia</a>
                <a>Trofeus</a>
                <a>Contato</a>
                <a>Sair</a>
            </div>
            <div class="hideSideBar" v-else>
                <a>
                    <i class="bi bi-person-circle"></i>
                    <span>Perfil</span>
                </a>
                <a>
                    <i class="bi bi-file-earmark-person"></i>
                    <span>Biografia</span>
                </a>
                <a>
                    <i class="bi bi-trophy-fill"></i>
                    <span>Trofeus</span>
                </a>
                <a>
                    <i class="bi bi-person-lines-fill"></i>
                    <span>Contato</span>
                </a>
                <a>
                    <i class="bi bi-box-arrow-left"></i>
                    <span>Sair</span>
                </a>
            </div>

        </div>

    </div>

</template>

<script lang="js">
export default {
    name: 'NavbarComponent',
    data() {
        localStorage.setItem('userImg', 'https://img.ifunny.co/images/0a01d9687a107ef307b0a774156a8964c8169b1e4278c6caa255a36acdaed809_1.webp')
        return {
            userImage: localStorage.getItem('userImg'),
            showSideBar: true,
            sideInOut: 'sideIn'
        }
    },
    methods: {
        chooseImage() { document.getElementById('choosePic').click() },
        injectNewPic() {
            localStorage.setItem('userImg', window.URL.createObjectURL(document.getElementById('choosePic').files[0]))
            this.userImage = localStorage.getItem('userImg')
        },
        showHideSideMenu() {
            this.showSideBar = !this.showSideBar

            if (this.showSideBar) this.sideInOut = 'sideIn'
            else this.sideInOut = 'sideOut'

        }
    }
}
</script>