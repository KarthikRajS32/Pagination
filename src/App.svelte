<script>
  // Sample data
  const columns = [
    { title: 'ID', key: 'id' },
    { title: 'Name', key: 'name' },
    { title: 'Age', key: 'age' },
    { title: 'Country', key: 'country'},

  ];

  const allRows = [
    { name: 'user1', age: 28, country: 'USA' },
    { name: 'user2', age: 34, country: 'Egypt' },
    { name: 'u3', age: 25, country: 'Japan' },
    { name: 'u4', age: 41, country: 'Mexico' },
    { name: 'u5', age: 30, country: 'Pakistan' },
    { name: 'u6', age: 28, country: 'USA' },
    { name: 'u7', age: 34, country: 'Egypt' },
    { name: 'u8', age: 25, country: 'Japan' },
    { name: 'u9', age: 41, country: 'Mexico' },
    { name: 'u10', age: 30, country: 'Pakistan' },
    { name: ' u11', age: 30, country: 'USA' },
    { name: 'u12', age: 32, country: 'Egypt' },
    { name: 'u13', age: 23, country: 'Japan' },
    { name: 'u14', age: 34, country: 'Mexico' },
    { name: 'u15', age: 35, country: 'Pakistan' },
    { name: 'u16', age: 27, country: 'USA' },
    { name: 'u17', age: 54, country: 'Egypt' },
    { name: 'u18', age: 54, country: 'Japan' },
    { name: 'u19', age: 67, country: 'Mexico' },
    { name: 'u20', age: 32, country: 'Pakistan' },
    { name: 'u21', age: 12, country: 'USA' },
    { name: 'u22', age: 56, country: 'Egypt' },
    { name: 'u23', age: 24, country: 'Japan' },
    { name: 'u24', age: 43, country: 'Mexico' },
    { name: 'u25', age: 32, country: 'Pakistan' },
    { name: 'u26', age: 53, country: 'USA' },
    { name: 'u27', age: 32, country: 'Egypt' },
    { name: 'u28', age: 53, country: 'Japan' },
    { name: 'u29', age: 34, country: 'Mexico' },
    { name: 'u30', age: 30, country: 'Pakistan' },
    { name: 'u31', age: 31, country: 'Paki' },
    { name: 'u32', age: 34, country: 'Pakis' }
  ].map((row, index) => ({ id: index + 1, ...row }));

  let currentPage = 1;
  const rowsPerPage = 10;
  const totalPages =Math.ceil(allRows.length / rowsPerPage);

  $: paginatedRows = allRows.slice(
    (currentPage - 1) * rowsPerPage,
    currentPage * rowsPerPage
  );

  function goToPage(page) {
    currentPage = page;
  }
</script>

<!-- Table Component -->
<table class="table-auto w-full h-full justify-center items-center text-center">
  <thead>
    <tr>
      {#each columns as { title }}
        <th class="px-4 py-2">{title}</th>
      {/each}
    </tr>
  </thead>
  <tbody>
    {#each paginatedRows as row}
      <tr>
        {#each columns as { key }}
          <td class="border px-4 py-2">{row[key]}</td>
        {/each}
      </tr>
    {/each}
  </tbody>
</table>

<!-- Pagination -->
<div class="flex gap-2 mt-4 justify-center items-center">
  <!-- Previous Button -->
  <button
    class="px-3 py-1 rounded text-blue-400 font-bold cursor-pointer"
    on:click={() => goToPage(currentPage - 1)}
    disabled={currentPage === 1}
  >
    ←Previous
  </button>

  <!-- Page Number Buttons -->
  {#each Array(totalPages) as _, index}
    <button
      class="px-3 py-1 rounded bg-blue-400 text-white hover:bg-blue-500 cursor-pointer"
      on:click={() => goToPage(index + 1)}
      class:selected={currentPage === index + 1}
    >
      {index + 1}
    </button>
  {/each}

  <!-- Next Button -->
  <button
    class="px-3 py-1 rounded text-blue-400 font-bold cursor-pointer"
    on:click={() => goToPage(currentPage + 1)}
    disabled={currentPage === totalPages}
  >
    Next→
  </button>
</div>

<style>
  button.selected {
    background-color: #1d4ed8; /* Darker blue */
    font-weight: bold;
  }
</style>
