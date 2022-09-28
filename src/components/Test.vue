<template>
  <button @click="generateReport">Download</button>
</template>

<script>
import jsPDF from "jspdf";
import autoTable from "jspdf-autotable";

export default {
  methods: {
    generateReport() {
      const doc = new jsPDF();

      autoTable(doc, {
        columnStyles: { europe: { halign: "center" } }, // European countries centered
        body: [
          { europe: "Sweden", america: "Canada", asia: "China" },
          { europe: "Norway", america: "Mexico", asia: "Japan" },
        ],
        columns: [
          { header: "Europe", dataKey: "europe" },
          { header: "Asia", dataKey: "asia" },
        ],
      });

      doc.save('table.pdf')
    },
  },
};
</script>

<style></style>
