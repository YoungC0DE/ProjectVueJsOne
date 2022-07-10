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

            <form class="d-flex justify-content-end w-50" role="search">
                <input class="form-control me-3" type="search" placeholder="pesquisar" aria-label="Search">
                <button class="btn btn-outline-success" type="submit">Buscar</button>
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
            <div class="hideSideBar d-flex row" v-else>
                <a>
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                        class="bi bi-person-circle" viewBox="0 0 16 16">
                        <path d="M11 6a3 3 0 1 1-6 0 3 3 0 0 1 6 0z" />
                        <path fill-rule="evenodd"
                            d="M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8zm8-7a7 7 0 0 0-5.468 11.37C3.242 11.226 4.805 10 8 10s4.757 1.225 5.468 2.37A7 7 0 0 0 8 1z" />
                    </svg> 
                    
                </a>
                <a>
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                        class="bi bi-file-earmark-person" viewBox="0 0 16 16">
                        <path d="M11 8a3 3 0 1 1-6 0 3 3 0 0 1 6 0z" />
                        <path
                            d="M14 14V4.5L9.5 0H4a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2zM9.5 3A1.5 1.5 0 0 0 11 4.5h2v9.255S12 12 8 12s-5 1.755-5 1.755V2a1 1 0 0 1 1-1h5.5v2z" />
                    </svg>
                    
                </a>
                <a>
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                        class="bi bi-trophy-fill" viewBox="0 0 16 16">
                        <path
                            d="M2.5.5A.5.5 0 0 1 3 0h10a.5.5 0 0 1 .5.5c0 .538-.012 1.05-.034 1.536a3 3 0 1 1-1.133 5.89c-.79 1.865-1.878 2.777-2.833 3.011v2.173l1.425.356c.194.048.377.135.537.255L13.3 15.1a.5.5 0 0 1-.3.9H3a.5.5 0 0 1-.3-.9l1.838-1.379c.16-.12.343-.207.537-.255L6.5 13.11v-2.173c-.955-.234-2.043-1.146-2.833-3.012a3 3 0 1 1-1.132-5.89A33.076 33.076 0 0 1 2.5.5zm.099 2.54a2 2 0 0 0 .72 3.935c-.333-1.05-.588-2.346-.72-3.935zm10.083 3.935a2 2 0 0 0 .72-3.935c-.133 1.59-.388 2.885-.72 3.935z" />
                    </svg>
                    
                </a>
                <a>
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                        class="bi bi-person-lines-fill" viewBox="0 0 16 16">
                        <path
                            d="M6 8a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-5 6s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1H1zM11 3.5a.5.5 0 0 1 .5-.5h4a.5.5 0 0 1 0 1h-4a.5.5 0 0 1-.5-.5zm.5 2.5a.5.5 0 0 0 0 1h4a.5.5 0 0 0 0-1h-4zm2 3a.5.5 0 0 0 0 1h2a.5.5 0 0 0 0-1h-2zm0 3a.5.5 0 0 0 0 1h2a.5.5 0 0 0 0-1h-2z" />
                    </svg>
                    
                </a>
                <a>
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                        class="bi bi-box-arrow-left" viewBox="0 0 16 16">
                        <path fill-rule="evenodd"
                            d="M6 12.5a.5.5 0 0 0 .5.5h8a.5.5 0 0 0 .5-.5v-9a.5.5 0 0 0-.5-.5h-8a.5.5 0 0 0-.5.5v2a.5.5 0 0 1-1 0v-2A1.5 1.5 0 0 1 6.5 2h8A1.5 1.5 0 0 1 16 3.5v9a1.5 1.5 0 0 1-1.5 1.5h-8A1.5 1.5 0 0 1 5 12.5v-2a.5.5 0 0 1 1 0v2z" />
                        <path fill-rule="evenodd"
                            d="M.146 8.354a.5.5 0 0 1 0-.708l3-3a.5.5 0 1 1 .708.708L1.707 7.5H10.5a.5.5 0 0 1 0 1H1.707l2.147 2.146a.5.5 0 0 1-.708.708l-3-3z" />
                    </svg>
                    
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*:focus {
    box-shadow: none !important;
}

.menu-enter-from,
.menu-leave-to {
    transition: all .3s ease-out 0;
}

.v-enter-from,
.v-leave-to {
    transition: all .2s ease-out .2s;
    opacity: 0;
}

.navBar {
    width: 100%;
    background-color: #0a1829;
    height: 8vh;
    padding: 5px 20px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    position: fixed;
    color: white;
    z-index: 1;
}

.navBar input {
    transition: .5s;
    background-color: #0a182900;
    border: 1px solid white;
    width: 30%;
}

.navBar svg {
    transition: none !important;
}

.navBar input:focus {
    background-color: white;
    width: 50%;
}

.sideIn {
    width: 20% !important;
}

.sideOut {
    width: 4% !important;
}

.navSider {
    transition: 0.2s;
    height: 100vh;
    background-color: #323e51;
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.containerTogglerBtn {
    width: 5%;
}

#sidebarBtn:hover {
    color: white;
    border-color: white;
}

#sidebarBtn {
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: center;
    align-items: center;
}

#sidebarBtn,
#sidebarBtn svg {
    transition: .5s;
    position: relative;
    width: 100%;
    height: 100%;
}

#sidebarBtn svg {
    width: 75%;
    height: 75%;
}

.userPicture {
    display: flex;
    flex-direction: column;
    align-content: center;
    align-items: center;
    justify-content: center;
}

.userPicture svg {
    position: absolute;
    width: 25px;
}

.userPicture img {
    width: 100px;
    height: 100px;
    transition: .5s;
    z-index: 1;
    object-fit: cover;
}

.userPicture img:hover {
    opacity: .5;
    cursor: pointer;
    z-index: 0;
}

.navSider .expandSideBar a {
    width: 100%;
    padding: 15px 0;
    border-radius: 4px;
    text-align: left;
    transition: .5s;
    text-align: center;
    overflow-x: hidden;
}

.navSider .hideSideBar span{
    display: flex;
}

.navSider .hideSideBar a {
    padding: 15px 0 15px 0;
    border-radius: 4px;
    text-align: center;
    transition: .5s;
}

.navSider .hideSideBar a:hover .navSider .hideSideBar span{
    display: flex;
    position: absolute;
}

.navSider a:hover {
    background-color: rgba(255, 255, 255, 0.25);
    cursor: pointer;
}
</style>
