<script lang="ts">

  import { ComponentRendererWrapper, SvelteTable } from "@guiexpert/svelte-table";
  import { ColumnDefIf, TableModelFactory } from "@guiexpert/table";
  import {
    applyBodyRenderer,
    createColumnDefs,
    createTableOptions,
    createTableRows
  } from "@guiexpert/demo-table-models";
  import { default as GenderRendererComponent } from "./GenderRendererComponent.svelte";

  const tableOptions = createTableOptions();
  const rows: SimplePersonIf[] = createTableRows();
  const columnDefs: ColumnDefIf[] = createColumnDefs();
  applyBodyRenderer(columnDefs[2], new ComponentRendererWrapper(GenderRendererComponent));
  const tableModel = TableModelFactory.buildByTypedRowsParam({
    rows,
    columnDefs,
    tableOptions,
    fixedLeftColumnCount: 0
  });

  function handleTableReady(api) {
    console.info("Table API:", api.detail);
  }

  function handleMouseClicked(evt) {
    console.info("Mouse clicked:", evt.detail);
  }
</script>

<main>
  <SvelteTable
    on:mouseClicked={handleMouseClicked}
    on:tableReady={handleTableReady}
    tableModel={tableModel}
    tableOptions={tableOptions}
  ></SvelteTable>
</main>

<style>
</style>
