```
npm install react @types/react typescript @chakra-ui/react @emotion/react @emotion/styled framer-motion @tanstack/react-table
```

```

// SortableTable.tsx
import React, { useMemo } from 'react';
import { useTable, useSortBy } from '@tanstack/react-table';
import { Table, Thead, Tbody, Tr, Th, Td, chakra, Box } from '@chakra-ui/react';

interface Fruit {
  id: number;
  name: string;
  size: string;
  count: number;
}

interface SortableTableProps {
  data: Fruit[];
}

const ChakraTh = chakra(Th, {
  baseStyle: { bg: 'gray.50', color: 'gray.700', fontWeight: 'bold' },
});

const ChakraTd = chakra(Td, {
  baseStyle: { bg: 'white', color: 'gray.700' },
});

const SortableTable = ({ data }: SortableTableProps) => {
  const columns = useMemo(
    () => [
      { Header: 'Name', accessor: 'name' },
      { Header: 'Size', accessor: 'size' },
      { Header: 'Count', accessor: 'count' },
    ],
    []
  );

  const { getTableProps, getTableBodyProps, headerGroups, rows, prepareRow } =
    useTable({ columns, data }, useSortBy);

  return (
    <Box overflowX="auto">
      <Table {...getTableProps()} width="full">
        <Thead>
          {headerGroups.map((headerGroup) => (
            <Tr {...headerGroup.getHeaderGroupProps()}>
              {headerGroup.headers.map((column) => (
                <ChakraTh {...column.getHeaderProps(column.getSortByToggleProps())}>
                  {column.render('Header')}
                  <chakra.span>
                    {column.isSorted ? (column.isSortedDesc ? ' ↓' : ' ↑') : ''}
                  </chakra.span>
                </ChakraTh>
              ))}
            </Tr>
          ))}
        </Thead>
        <Tbody {...getTableBodyProps()}>
          {rows.map((row) => {
            prepareRow(row);
            return (
              <Tr {...row.getRowProps()}>
                {row.cells.map((cell) => (
                  <ChakraTd {...cell.getCellProps()}>{cell.render('Cell')}</ChakraTd>
                ))}
              </Tr>
            );
          })}
        </Tbody>
      </Table>
    </Box>
  );
};

export default SortableTable;

```

```
// App.tsx
import React from 'react';
import SortableTable from './SortableTable';

const list = [
  { id: 0, name: 'りんご', size: 'L', count: 3 },
  { id: 1, name: 'みかん', size: 'M', count: 5 },
  { id: 2, name: 'バナナ', size: 'S', count: 2 },
];

const App: React.FC = () => {
  return (
    <div>
      <SortableTable data={list} />
    </div>
  );
};

export default App;

```


