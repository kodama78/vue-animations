<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animations</h1>
                <hr>
                <select name="" id="" v-model="alertAnimation" class="form-control">
                    <option value="fade">Fade</option>
                    <option value="slide">Slide</option>
                </select>
                <button class="btn btn-primary" @click="show = !show">Show Alert</button>
                <br><br>
                <transition :name="alertAnimation">
                    <div class="alert alert-info" v-if="show">This is some info</div>
                </transition>
                <transition name="slide" type="animation">
                    <div class="alert alert-info" v-if="show">This is some info</div>
                </transition>
                <transition enter-class=""
                            enter-active-class="animated bounce"
                            leave-class=""
                            leave-active-class="animated shake"
                            appear >
                    <div class="alert alert-info" v-if="show">This is some info</div>
                </transition>
                <transition :name="alertAnimation" mode="out-in">
                    <div class="alert alert-info" v-if="show" key="info">This is some info</div>
                    <div class="alert alert-warning" v-else key="warning">This is some warning</div>
                </transition>
                <hr>
                <button class="btn btn-primary" @click="load = !load">Load / Remove Element</button>
                <br><br>
                <transition @before-enter="beforeEnter"
                            @enter="enter"
                            @after-enter="afterEnter"
                            @enter-cancelled="enterCancelled"

                            @before-leave="beforeLeave"
                            @leave="leave"
                            @after-lave="afterLeave"
                            @leave-cancelled="leaveCancelled"
                            :css="false">
                    <div style="width: 100px; height: 100px; background-color: lightgreen" v-if="load"></div>
                </transition>
                <hr>
                <button class="btn btn-primary" @click="selectedComponent === 'SuccessAlert' ? selectedComponent = 'DangerAlert' : selectedComponent = 'SuccessAlert'">Toggle Components</button>
                <br><br>
                <transition name="fade" mode="out-in">
                    <component :is="selectedComponent"></component>
                </transition>
                <hr>
                <button class="btn btn-primary" @click="addItem">Add Item</button>
                <br><br>
                <ul class="list-group">
                    <transition-group name="slide">
                        <li class="list-group-item"
                            v-for="(number, index) in numbers"
                            :key="number"
                            @click="removeItem(index)">
                            {{ number }}
                        </li>
                    </transition-group>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    import DangerAlert from './DangerAlert.vue';
    import SuccessAlert from './SuccessAlert.vue';

    export default {
        data() {
            return {
                show: true,
                alertAnimation: 'fade',
                elementWidth: 100,
                selectedComponent: 'SuccessAlert',
                load: true,
                numbers: [1, 2, 3, 4, 5]
            }
        },
        methods: {
            beforeEnter(el) {
                this.elementWidth = 100;
                el.style.width = this.elementWidth + 'px';
            },
            enter(el, done) {
                let round = 1;
                const interval = setInterval(() => {
                    el.style.width = (this.elementWidth + round * 10) + 'px';
                    round++;
                    if (round > 20) {
                        clearInterval(interval);
                        done();
                    }
                }, 20);
                done();
            },
            afterEnter(el) {

            },
            enterCancelled(el) {

            },
            beforeLeave(el) {
                this.elementWidth = 300;
                el.style.width = this.elementWidth + 'px';
            },
            leave(el, done) {
                let round = 1;
                const interval = setInterval(() => {
                    el.style.width = (this.elementWidth - round * 10) + 'px';
                    round++;
                    if (round > 20) {
                        clearInterval(interval);
                        done();
                    }
                }, 20);
            },
            afterLeave(el) {

            },
            leaveCancelled(el) {

            },
            addItem() {
                const pos = Math.floor(Math.random() * this.numbers.length);
                this.numbers.splice(pos, 0, this.numbers.length + 1);
            },
            removeItem(index) {
                this.numbers.splice(index, 1);
            }

        },
        components: {
            DangerAlert,
            SuccessAlert
        }
    }
</script>

<style>
    .fade-enter {
        opacity: 0;
    }

    .fade-enter-active {
        transition: opacity 1s;
    }

    .fade-leave {

    }

    .fade-leave-active {
        transition: opacity 1s;
        opacity: 0;
    }

    .slide-enter {
        opacity: 0;
    }

    .slide-enter-active {
        -webkit-animation: slide-in 1s ease-out forwards;
        -o-animation: slide-in 1s ease-out forwards;
        animation: slide-in 1s ease-out forwards;
        -webkit-transition: opacity .5s;
        -moz-transition: opacity .5s;
        -ms-transition: opacity .5s;
        -o-transition: opacity .5s;
        transition: opacity .5s;
    }

    .slide-leave {
        
    }

    .slide-leave-active {
        -webkit-animation: slide-out 1s ease-out forwards;
        -o-animation: slide-out 1s ease-out forwards;
        animation: slide-out 1s ease-out forwards;
        -webkit-transition: opacity 1s;
        -moz-transition: opacity 1s;
        -ms-transition: opacity 1s;
        -o-transition: opacity 1s;
        transition: opacity 1s;
        opacity: 0;
        position: absolute;
    }

    .slide-move {
        transition: transform 1s;
    }

    @keyframes slide-in {
        from {
            transform: translateY(20px);
        }
        to {
            transform: translateY(0);
        }
    }

    @keyframes slide-out {
        from {
            transform: translateY(0);
        }
        to {
            transform: translateY(20px);
        }
    }
</style>
