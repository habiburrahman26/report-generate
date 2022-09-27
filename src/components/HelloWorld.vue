<script>
import { jsPDF } from "jspdf";
import autoTable from "jspdf-autotable";

const DUMMY_data = [
  {
    id: "632804c7fc13ae0943000434",
    full_name: "Nerty McClean",
    total_cost: 10172,
    paid_amount: 323,
    bill_created_at: "2010-04-08T12:31:58.000Z",
  },
  {
    id: "632804c7fc13ae0943000435",
    full_name: "Melisse Dakers",
    total_cost: 22172,
    paid_amount: 194,
    bill_created_at: "2010-07-26T13:01:38.000Z",
  },
  {
    id: "632804c7fc13ae0943000436",
    full_name: "Louisa Medley",
    total_cost: 4876,
    paid_amount: 2335,
    bill_created_at: "2013-12-12T21:26:11.000Z",
  },
  {
    id: "632804c7fc13ae0943000437",
    full_name: "Laney Poinsett",
    total_cost: 10404,
    paid_amount: 356,
    bill_created_at: "2011-12-12T05:37:08.000Z",
  },
  {
    id: "632804c7fc13ae0943000438",
    full_name: "Aeriell O'Feeny",
    total_cost: 14564,
    paid_amount: 147,
    bill_created_at: "2012-10-07T11:39:34.000Z",
  },
  {
    id: "632804c7fc13ae0943000439",
    full_name: "Neysa Killen",
    total_cost: 41988,
    paid_amount: 137,
    bill_created_at: "2012-06-06T11:55:14.000Z",
  },
  {
    id: "632804c7fc13ae094300043a",
    full_name: "Valerye Lednor",
    total_cost: 4219,
    paid_amount: 232,
    bill_created_at: "2015-06-20T07:36:02.000Z",
  },
  {
    id: "632804c7fc13ae094300043b",
    full_name: "Tucky Bartod",
    total_cost: 8365,
    paid_amount: 6243,
    bill_created_at: "2013-12-29T12:28:42.000Z",
  },
  {
    id: "632804c7fc13ae094300043c",
    full_name: "Shelba Spanswick",
    total_cost: 4944,
    paid_amount: 206,
    bill_created_at: "2016-08-27T06:11:09.000Z",
  },
  {
    id: "632804c7fc13ae094300043d",
    full_name: "Neal Yacob",
    total_cost: 487,
    paid_amount: 346,
    bill_created_at: "2020-03-07T14:49:39.000Z",
  },
  {
    id: "632804c7fc13ae094300043e",
    full_name: "Jobina Saller",
    total_cost: 7832,
    paid_amount: 139,
    bill_created_at: "2006-08-27T22:00:56.000Z",
  },
  {
    id: "632804c7fc13ae094300043f",
    full_name: "Francyne Prium",
    total_cost: 3180,
    paid_amount: 345,
    bill_created_at: "2003-11-24T18:06:12.000Z",
  },
  {
    id: "632804c7fc13ae0943000440",
    full_name: "Lonnie Blackborn",
    total_cost: 4861,
    paid_amount: 4308,
    bill_created_at: "2013-09-16T15:18:32.000Z",
  },
  {
    id: "632804c7fc13ae0943000441",
    full_name: "Marla Tilby",
    total_cost: 373,
    paid_amount: 373,
    bill_created_at: "2004-03-18T15:07:18.000Z",
  },
  {
    id: "632804c7fc13ae0943000442",
    full_name: "Shurlocke Winchurch",
    total_cost: 551,
    paid_amount: 284,
    bill_created_at: "2006-08-29T03:27:08.000Z",
  },
  {
    id: "632804c7fc13ae0943000443",
    full_name: "Danita Hedderly",
    total_cost: 4881,
    paid_amount: 190,
    bill_created_at: "2003-12-27T15:50:35.000Z",
  },
  {
    id: "632804c7fc13ae0943000444",
    full_name: "Odie Tonkinson",
    total_cost: 43997,
    paid_amount: 112,
    bill_created_at: "2008-07-15T01:54:38.000Z",
  },
  {
    id: "632804c7fc13ae0943000445",
    full_name: "Vaughn Senogles",
    total_cost: 3153,
    paid_amount: 373,
    bill_created_at: "2006-04-16T11:42:15.000Z",
  },
  {
    id: "632804c7fc13ae0943000446",
    full_name: "Torrance Bourges",
    total_cost: 25450,
    paid_amount: 245,
    bill_created_at: "2014-02-28T05:56:29.000Z",
  },
];

export default {
  data() {
    return {
      revenue: DUMMY_data,
    };
  },
  methods: {
    generatePdf() {
      const doc = new jsPDF();

      const today = new Date();
      const yyyy = today.getFullYear();
      let mm = today.getMonth() + 1; // Months start at 0!
      let dd = today.getDate();

      if (dd < 10) dd = "0" + dd;
      if (mm < 10) mm = "0" + mm;

      const formattedToday = dd + "/" + mm + "/" + yyyy;

      autoTable(doc, {
        head: [["Id", "Name", "Total Cost", "Paid Amount"]],
        body: [...this.makeObjectToArray()],
      });

      doc.setFontSize(10);
      doc.text("Revenue", 14, 10);
      doc.text(`Date: ${formattedToday}`, 165, 10);
      doc.save("table.pdf");
    },
    makeObjectToArray() {
      const newRevenue = [];

      for (const item of this.revenue) {
        const arr = [
          item.id,
          item.full_name,
          item.total_cost,
          item.paid_amount,
        ];
        newRevenue.push(arr);
      }

      return newRevenue;
    },
  },
  mounted() {},
};
</script>

<template>
  <button @click="generatePdf">Download</button>
  <table id="customers">
    <thead>
      <th>Id</th>
      <th>Name</th>
      <th>Paid Amount</th>
      <th>Total Cost</th>
      <th>Date</th>
    </thead>
    <tbody>
      <tr v-for="item in revenue" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.full_name }}</td>
        <td>{{ item.paid_amount }}</td>
        <td>{{ item.total_cost }}</td>
        <td>{{ new Date(item.bill_created_at).getFullYear() }}</td>
      </tr>
    </tbody>
  </table>
</template>

<style>
#customers {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#customers td,
#customers th {
  border: 1px solid #ddd;
  padding: 8px;
}

#customers tr:nth-child(even) {
  background-color: #f2f2f2;
}

#customers tr:hover {
  background-color: #ddd;
}

#customers th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #6a6e6d;
  color: white;
}

button {
  margin-bottom: 10px;
}
</style>
