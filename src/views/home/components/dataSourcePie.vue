<template>
    <div style="width:100%;height:100%;" id="data_source_con"></div>
</template>

<script>
import echarts from 'echarts';

export default {
    name: 'dataSourcePie',
    data () {
        return {
            nodes: [
                {
                    name:'1',
                    value: 0,
                    label: {
                            normal: {
                                show: true,
                                position: 'bottom',
                                fontSize: '12'
                        }
                    },
                    symbol: 'image://http://oow60tecr.bkt.clouddn.com/firewall.png',
                    symbolSize: [40, 40],
                    x:300,
                    y:120
                },
                {
                    name:'2',
                    value: 1,
                    label: {
                            normal: {
                                show: true,
                                position: 'bottom',
                                fontSize: '12'
                        }
                    },
                    symbol: 'image://http://oow60tecr.bkt.clouddn.com/firewall.png',
                    symbolSize: [40, 40],
                    x:600,
                    y:170
                }
            ],
            links: []
        }
        
    },
    mounted () {
        this.links = this.nodes.map(function (item, idx) {
            return {
                source: idx,
                target: idx + 1
            };
        })
        this.$nextTick(() => {
            var dataSourcePie = echarts.init(document.getElementById('data_source_con'));
            const option = {
                title: {
                    text: '',
                },
                tooltip:{}, 
                // animationDurationUpdate: 10,
                // animationEasingUpdate: 'quinticInOut',
                animationEasing: 'elasticOut',
                animationDelayUpdate: function (idx) {
                    return idx * 1;
                },
                grid: {       
                    y: '0',
                    y2: '0',
                    x: '0',
                    x2: '0'
                },
                xAxis: {
                    type: 'value',
                    position: 'top',
                },
                yAxis: {
                    inverse: true,
                    type: 'value',
                },
                silent: true,
                series : [
                    {
                        type: 'graph',
                        layout: 'none',
                        symbolSize: 50,            
                        roam: true,                
                        focusNodeAdjacency:true,   
                        label: {
                            normal: {
                                show: true,       
                                position:'top',
                                fontSize:20
                            }
                        },
                        legend: {  
                            left: 'left',  
                            data:['h1','h2', 'h3']  
                        },
                        edgeSymbol: ['circle', 'circle'],
                        edgeSymbolSize: [1, 1],   
                        edgeLabel: {
                            normal:{
                                show:false
                            },
                            emphasis: {
                                textStyle: {
                                    fontSize: 20   
                                }
                            }
                        },
                        animationDelay: function (idx) {
                        return idx * 300;
                        },
                        force: {
                            edgeLength: 5,
                            repulsion: 20,
                            gravity: 0.2
                        },
                        //节点信息
                        data: [],
                        links: [],
                        lineStyle: {
                            normal: {
                                show:true,
                                color: {       
                                    type: 'linear',
                                    x: 0,
                                    y: 0,
                                    x2: 0,
                                    y2: 1,
                                    colorStops: [
                                        {
                                            offset: 0, color: 'red'
                                        }
                                        ,{
                                            offset: 1, color: 'blue' 
                                        }
                                    ],
                                    globalCoord: false
                                },     
                            },
                            emphasis:{
                                color:'red',
                                width:3,
                                type:'dashed',
                            }
                        },      
                        tooltip: {
                            position:'bottom',                      
                            backgroundColor:'green',
                            textStyle:{
                                fontSize:18,
                            }
                        }
                    }
                ]
            };
            option.series[0].data = this.nodes;
            option.series[0].links = this.links;
            dataSourcePie.setOption(option);
            window.addEventListener('resize', function () {
                dataSourcePie.resize();
            });
        });
    }
};
</script>
