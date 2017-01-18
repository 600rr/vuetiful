<template>
    <div id="datatables" class="container">
        <h1>Datatables</h1>
        <input type="checkbox" v-model="customers.editable">
        <div class="grid-row" layout="row top-stretch">
            <div class="grid-cell">
                <datatable id="data-table-1" :columns="customers.columns" :rows="customers.rows" :editable="customers.editable">
                    <template slot="surname" scope="cell">
                        <div class="surname">{{ cell.value }}</div>
                    </template>
                    <template slot="dateOfBirth" scope="cell">
                        <datetime-picker v-model="cell.value" v-if="customers.editable"></datetime-picker>
                        <span class="date-of-birth" v-else>{{ cell.column.formatter(cell.value) }}</span>
                    </template>
                </datatable>
            </div>
        </div>
        <div class="grid-row" layout="row top-stretch">
            <div class="grid-cell">
                <datatable id="data-table-1" :columns="customers.columns" :rows="customers.rows" :editable="customers.editable">
                    <template slot="surname" scope="cell">
                        <div class="surname">{{ cell.value }}</div>
                    </template>
                    <template slot="dateOfBirth" scope="cell">
                        <datetime-picker v-model="cell.value" v-if="customers.editable"></datetime-picker>
                        <span class="date-of-birth" v-else>{{ cell.column.formatter(cell.value) }}</span>
                    </template>
                </datatable>
            </div>
            <div class="grid-cell">
                <datatable id="data-table-2" :columns="customers.columns" :rows="customers.rows" :editable="customers.editable">
                    <template slot="surname" scope="cell">
                        <div class="surname">{{ cell.value }}</div>
                    </template>
                    <template slot="dateOfBirth" scope="cell">
                        <datetime-picker v-model="cell.value" v-if="customers.editable"></datetime-picker>
                        <span class="date-of-birth" v-else>{{ cell.column.formatter(cell.value) }}</span>
                    </template>
                </datatable>
            </div>
        </div>
    </div>
</template>

<script>
    import { format } from "date-fns";

    let customers = {
        editable: false,
        columns: [
            {
                key: "givenName",
                label: "Given Name"
            },
            {
                key: "surname",
                label: "Surname"
            },
            {
                key: "email",
                label: "Email",
                width: 33
            },
            {
                key: "dateOfBirth",
                label: "Date of Birth",
                formatter: value => format(value, "DD MMMM YYYY")
            }
        ],
        rows: []
    };

    export default {
        data() {

            let rows = [];

            for (let i = 0; i < 10; i++) {
                rows.push({
                    givenName: "John " + i,
                    surname: "Smith " + i,
                    email: `john${i}.smith${i}@random.com`,
                    dateOfBirth: new Date()
                });
            }

            customers.rows = rows.reverse();

            return {
                customers: customers
            }
        }
    }
</script>