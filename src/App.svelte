<script lang="ts">

  import { ComponentRendererWrapper, GuiexpertTable } from "@guiexpert/svelte-table";
  import { ColumnDefIf, TreeFactory } from "@guiexpert/table";
  import {
    applyBodyRenderer,
    createColumnDefs,
    createTableOptions,
    createTableRows, SimplePersonIf
  } from "@guiexpert/demo-table-models";
  import { default as GenderRendererComponent } from "./GenderRendererComponent.svelte";

  const tableOptions = createTableOptions();
  const rows: SimplePersonIf[] = createTableRows();
  const columnDefs: ColumnDefIf[] = createColumnDefs();
  applyBodyRenderer(columnDefs[2], new ComponentRendererWrapper(GenderRendererComponent));
  const tableModel = TreeFactory.buildByTypedRowsParam({
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
  <GuiexpertTable
    on:mouseClicked={handleMouseClicked}
    on:tableReady={handleTableReady}
    tableModel={tableModel}
    tableOptions={tableOptions}
  ></GuiexpertTable>
</main>

<style>
</style>
