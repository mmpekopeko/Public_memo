
```tsx
import React from 'react';
import {
  useTable,
  useSortBy,
  usePagination,
  TableInstance,
  Column,
} from '@tanstack/react-table';
import { ChakraProvider, Table, Tbody, Tr, Td, Th, VStack } from '@chakra-ui/react';

const columns: Column[] = [
  { Header: 'ID', accessor: 'id' },
  { Header: '名前', accessor: 'name' },
  { Header: 'サイズ', accessor: 'size' },
  { Header: '個数', accessor: 'count' },
];

const list = [
  { id: 0, name: 'りんご', size: 'L', count: 3 },
  { id: 1, name: 'みかん', size: 'M', count: 5 },
  { id: 2, name: 'バナナ', size: 'S', count: 2 },
];

const MyTable = ({ columns, data }: { columns: Column[]; data: any[] }) => {
  const {
    getTableProps,
    getTableBodyProps,
    headerGroups,
    page,
    nextPage,
    previousPage,
    canNextPage,
    canPreviousPage,
  } = useTable(
    {
      columns,
      data,
    },
    useSortBy,
    usePagination
  ) as TableInstance;

  return (
    <VStack align="stretch" spacing="4">
      <Table {...getTableProps()} variant="simple">
        <thead>
          {headerGroups.map((headerGroup) => (
            <Tr {...headerGroup.getHeaderGroupProps()}>
              {headerGroup.headers.map((column) => (
                <Th {...column.getHeaderProps(column.getSortByToggleProps())}>
                  {column.render('Header')}
                  <span>
                    {column.isSorted ? (column.isSortedDesc ? ' 🔽' : ' 🔼') : ''}
                  </span>
                </Th>
              ))}
            </Tr>
          ))}
        </thead>
        <Tbody {...getTableBodyProps()}>
          {page.map((row) => (
            <Tr {...row.getRowProps()}>
              {row.cells.map((cell) => (
                <Td {...cell.getCellProps()}>{cell.render('Cell')}</Td>
              ))}
            </Tr>
          ))}
        </Tbody>
      </Table>
      <div>
        <button onClick={() => previousPage()} disabled={!canPreviousPage}>
          Previous Page
        </button>
        <button onClick={() => nextPage()} disabled={!canNextPage}>
          Next Page
        </button>
      </div>
    </VStack>
  );
};

const App = () => {
  return (
    <ChakraProvider>
      <MyTable columns={columns} data={list} />
    </ChakraProvider>
  );
};

export default App;

```
