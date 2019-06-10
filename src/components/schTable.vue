<template>
    <div id="sch">
        <div class="title">
            <span>Schedule Table</span>
        </div>
        <div class="sch-head">
            <div class="date">
                <el-date-picker v-model="dateVal" type="date" placeholder="Pick a day" :clearable="false"
                    @change="getDate" style="width:140px">
                </el-date-picker>
                <span class='words'>From&nbsp;{{headStart}}&nbsp;To&nbsp;{{headEnd}}</span>
            </div>

            <el-button-group class="week">
                <el-button class='weekBtn' :class="{'is-active':moveCount<0}" @click="lastWeek"><i
                        class="el-icon-arrow-left"></i>Last{{moveCount<0?Math.abs(moveCount):''}}Week</el-button>
                <el-button class='weekBtn' :class="{'is-active':moveCount==0}" @click="thisWeek">This Week</el-button>
                <el-button class='weekBtn' :class="{'is-active':moveCount>0}" @click="nextWeek">
                    Next{{moveCount>0?Math.abs(moveCount):''}}Week<i class="el-icon-arrow-right el-icon--right"></i>
                </el-button>
            </el-button-group>

        </div>

        <div class="sch-table">
            <el-table style="width: 100%" :data="finalTable" border>
                <el-table-column min-width="120px" show-overflow-tooltip>
                    <template slot="header" slot-scope='scope'>
                        <label style="float:left">Monday</label>
                        <span>{{(weekDate[0])}}</span>
                    </template>
                    <template slot-scope="scope">
                        <span>{{(scope.row.wk1)}}</span>
                    </template>
                </el-table-column>
                <el-table-column prop="tues" min-width="120px" show-overflow-tooltip>
                    <template slot="header" slot-scope='scope'>
                        <label style="float:left">Tuesday</label>
                        <span>{{weekDate[1]}}</span>
                    </template>
                    <template slot-scope="scope">
                        <span>{{(scope.row.wk2)}}</span>
                    </template>
                </el-table-column>
                <el-table-column prop="wens" min-width="120px" show-overflow-tooltip>
                    <template slot="header" slot-scope='scope'>
                        <label style="float:left">Wednesday</label>
                        <span>{{weekDate[2]}}</span>
                    </template>
                    <template slot-scope="scope">
                        <span>{{(scope.row.wk3)}}</span>
                    </template>
                </el-table-column>
                <el-table-column prop="thurs" min-width="120px" show-overflow-tooltip>
                    <template slot="header" slot-scope='scope'>
                        <label style="float:left">Thursday</label>
                        <span>{{weekDate[3]}}</span>
                    </template>
                    <template slot-scope="scope">
                        <span>{{(scope.row.wk4)}}</span>
                    </template>
                </el-table-column>
                <el-table-column prop="fri" min-width="120px" show-overflow-tooltip>
                    <template slot="header" slot-scope='scope'>
                        <label style="float:left">Friday</label>
                        <span>{{weekDate[4]}}</span>
                    </template>
                    <template slot-scope="scope">
                        <span>{{(scope.row.wk5)}}</span>
                    </template>
                </el-table-column>
                <el-table-column prop="sat" min-width="120px" show-overflow-tooltip>
                    <template slot="header" slot-scope='scope'>
                        <label style="float:left">Saturday</label>
                        <span>{{weekDate[5]}}</span>
                    </template>
                    <template slot-scope="scope">
                        <span>{{(scope.row.wk6)}}</span>
                    </template>
                </el-table-column>
                <el-table-column prop="sun" min-width="120px" show-overflow-tooltip>
                    <template slot="header" slot-scope='scope'>
                        <label style="float:left">Sunday</label>
                        <span>{{weekDate[6]}}</span>
                    </template>
                    <template slot-scope="scope">
                        <span>{{(scope.row.wk7)}}</span>
                    </template>
                </el-table-column>
            </el-table>
        </div>

    </div>

</template>

<script>
    const finalTable = [{ wk1: 'html', wk2: 'css', wk3: 'js', wk4: 'vue', wk5: 'react', wk6: 'flutter', wk7: 'python' }];
    export default {
        name: "scheduleTable",
        data: function () {
            return {
                finalTable,
                weekDate: [],
                dateVal: '',
                weekStart: '',
                weekEnd: '',
                headStart: '',
                headEnd: '',
                moveCount: 0,
            };
        },

        created() { },

        mounted() {
            //load default week
            this.loadData();  //load default week 
        },

        methods: {
            loadData: function () {
                //set this week as default week
                this.dateVal = new Date();
                this.thisWeek();
            },


            getDate: function (val) {
                let startDate = new Date();
                let endDate = new Date();
                let date = (val.toString()).substr(0, 3)
                // get start date and end date 
                if (date == 'Mon') {
                    startDate.setTime(val.getTime() - 3600 * 1000 * 24 * 0);
                    endDate.setTime(val.getTime() + 3600 * 1000 * 24 * 6);
                }
                if (date == 'Tue') {
                    startDate.setTime(val.getTime() - 3600 * 1000 * 24 * 1);
                    endDate.setTime(val.getTime() + 3600 * 1000 * 24 * 5);
                }
                if (date == 'Wed') {
                    startDate.setTime(val.getTime() - 3600 * 1000 * 24 * 2);
                    endDate.setTime(val.getTime() + 3600 * 1000 * 24 * 4);
                }
                if (date == 'Thu') {
                    startDate.setTime(val.getTime() - 3600 * 1000 * 24 * 3);
                    endDate.setTime(val.getTime() + 3600 * 1000 * 24 * 3);
                }
                if (date == 'Fri') {
                    startDate.setTime(val.getTime() - 3600 * 1000 * 24 * 4);
                    endDate.setTime(val.getTime() + 3600 * 1000 * 24 * 2);
                }
                if (date == 'Sat') {
                    startDate.setTime(val.getTime() - 3600 * 1000 * 24 * 5);
                    endDate.setTime(val.getTime() + 3600 * 1000 * 24 * 1);
                }
                if (date == 'Sun') {
                    startDate.setTime(val.getTime() - 3600 * 1000 * 24 * 6);
                    endDate.setTime(val.getTime() + 3600 * 1000 * 24 * 0);
                }
                let dateFrom = this.calDate(startDate)
                let dateEnd = this.calDate(endDate)
                this.weekStart = startDate;
                this.weekEnd = endDate;
                this.headStart = this.calDay(startDate)
                this.headEnd = this.calDay(endDate)

                this.calWeek(startDate);
            },

            //week selection function
            lastWeek: function () {
                this.moveCount--;
                let lastMon = new Date();
                lastMon = new Date(lastMon.setTime(this.weekStart.getTime() - 3600 * 1000 * 24 * 7));
                this.getDate(lastMon)
            },

            thisWeek: function () {
                this.moveCount = 0;
                let thisWeek = new Date()
                this.getDate(thisWeek);
            },

            nextWeek: function () {
                this.moveCount++;
                let nextMon = new Date();
                nextMon = new Date(nextMon.setTime(this.weekStart.getTime() + 3600 * 1000 * 24 * 7))
                this.getDate(nextMon)
            },

            //calculate date form monday to sunday
            calWeek: function (val) {
                this.weekDate = [];
                for (var i = 0; i < 7; i++) {
                    let headerTime = new Date()
                    headerTime.setTime(val.getTime() + 3600 * 1000 * 24 * i);
                    headerTime = this.calDate(headerTime)
                    this.weekDate[i] = headerTime;
                }
            },

            //format date
            calDate: function (val) {
                var seperator1 = "-";
                var cover1 = "(";
                var cover2 = ")";
                var month = val.getMonth() + 1;
                var strDate = val.getDate();
                if (month >= 1 && month <= 9) {
                    month = "0" + month;
                }
                if (strDate >= 0 && strDate <= 9) {
                    strDate = "0" + strDate;
                }
                var currentdate = cover1 + month + seperator1 + strDate + cover2;
                return currentdate;
            },

            calDay: function (val) {
                var seperator1 = "-";
                var seperator2 = ":";
                var month = val.getMonth() + 1;
                var strDate = val.getDate();
                if (month >= 1 && month <= 9) {
                    month = "0" + month;
                }
                if (strDate >= 0 && strDate <= 9) {
                    strDate = "0" + strDate;
                }
                var currentdate = val.getFullYear() + seperator1 + month + seperator1 + strDate;
                return currentdate;
            },
        }
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    #sch {
        padding: 0 20px;
    }

    #sch .title {
        width: 100%;
        font-size: 20px;
        font-weight: bold;
        text-align: center;
        padding: 10px 0;
        border-bottom: 1px solid #F1F2F7;
    }

    #sch .sch-head {
        padding-top: 10px;
        min-height: 40px;
    }

    #sch .sch-head .date {
        float: left;
    }

    #sch .sch-head .date .words {
        display: inline-block;
        margin-left: 20px;
        color: #303133;
        font-size: 16px;
    }

    #sch .sch-head .week {
        float: right;
    }

    #sch .weekBtn {
        padding: 0;
        width: 100px;
        height: 40px;
        min-width: 60px;
        color: #606266;
        font-size: 14px;
        border: 1px solid #DCDFE6;
    }

    #sch .is-active {
        color: #fff;
        background-color: #1E88E5;
        border-color: #1E88E5;
    }

    #sch .weekBtn:hover {
        background-color: #1E88E5;
        border-color: #1E88E5;
        color: #fff;
    }

    #sch .sch-table {
        margin-top: 10px;
    }
</style>