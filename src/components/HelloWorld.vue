<template>
    <div>
        <el-dialog title="收货地址" :visible.sync="dialogFormVisible">
            <el-button type="primary" @click="init()">init</el-button>
            <el-button type="primary" @click="isShow=true">aaa</el-button>
        </el-dialog>

        <div class="reveal" v-if="isShow" style="height: 800px; margin: 0">
            <div class="slides">
                <section>
                    <h2>图</h2>
                    <div id="pieReport" style="height: 600px; width: 600px;"></div>
                </section>
                <section>
                    <el-card class="box-card">
                        <div slot="header" class="clearfix">
                            <span>卡片名称</span>
                            <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>
                        </div>
                        <div v-for="o in 4" :key="o" class="text item">
                            {{'列表内容 ' + o }}
                        </div>
                    </el-card>
                    <h2>Stretch Example</h2>
                    <p>Image byline</p>
                </section>
                <section>Horizontal Slide</section>
                <section>
                    <section>Vertical Slide 1</section>
                    <section>Vertical Slide 1</section>
                    <section>Vertical Slide 1</section>
                </section>
                <section>Horizontal Slide</section>
                <section>
                    <section>Vertical Slide 1</section>
                    <section>Vertical Slide 1</section>
                    <section>Vertical Slide 1</section>
                </section>
                <section>Horizontal Slide</section>
            </div>
        </div>
    </div>
</template>

<script>
    import 'reveal.js/dist/reveal.css'
    import 'reveal.js/dist/theme/white.css'

    import Reveal from 'reveal.js'

    import Echarts from 'echarts'

    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                dialogFormVisible: true,
                isShow: false,
                charts: "",
                opinion: ["及格人数", "未及格人数"],
                opinionData: [
                    {value: 12, name: "及格人数", itemStyle: "#1ab394"},
                    {value: 18, name: "未及格人数", itemStyle: "#79d2c0"}
                ]
            }
        },
        methods: {
            init() {
                new Reveal().initialize();
                this.drawPie("pieReport");
            },
            drawPie(id) {
                this.charts = Echarts.init(document.getElementById(id));
                this.charts.setOption({
                    tooltip: {
                        trigger: "item",
                        formatter: "{a}<br/>{b}:{c} ({d}%)"
                    },
                    legend: {
                        bottom: 10,
                        left: "center",
                        data: this.opinion
                    },
                    series: [
                        {
                            name: "状态",
                            type: "pie",
                            radius: "65%",
                            center: ["50%", "50%"],
                            avoidLabelOverlap: false,
                            itemStyle: {
                                emphasis: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: "rgba(0, 0, 0, 0.5)"
                                },
                                color: function (params) {
                                    //自定义颜色
                                    var colorList = ["#1ab394", "#79d2c0"];
                                    return colorList[params.dataIndex];
                                }
                            },
                            data: this.opinionData
                        }
                    ]
                });
            },
        },
        created() {
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
