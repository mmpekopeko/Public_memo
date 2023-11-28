```tsx

import * as React from 'react';
import { useTable } from 'react-table';
import { ChakraProvider, Table, Thead, Tbody, Tr, Th, Td } from '@chakra-ui/react';

// データの例
const data = [
  { name: 'Item 1', size: 20 },
  { name: 'Item 2', size: 15 },
  { name: 'Item 3', size: 25 },
];

const TableComponent = () => {
  // テーブルの設定
  const columns = React.useMemo(
    () => [
      { Header: 'Name', accessor: 'name' },
      { Header: 'Size', accessor: 'size' },
    ],
    []
  );

  const { getTableProps, getTableBodyProps, headerGroups, rows, prepareRow } = useTable(
    { columns, data },
    // useSortBy は変更されて以下のように使います
    useSortBy
  );

  return (
    <Table {...getTableProps()} variant="simple">
      <Thead>
        {headerGroups.map(headerGroup => (
          <Tr {...headerGroup.getHeaderGroupProps()}>
            {headerGroup.headers.map(column => (
              <Th {...column.getHeaderProps(column.getSortByToggleProps())}>
                {column.render('Header')}
                {/* ソートアイコン */}
                {column.isSorted ? (column.isSortedDesc ? ' ↓' : ' ↑') : ''}
              </Th>
            ))}
          </Tr>
        ))}
      </Thead>
      <Tbody {...getTableBodyProps()}>
        {rows.map(row => {
          prepareRow(row);
          return (
            <Tr {...row.getRowProps()}>
              {row.cells.map(cell => (
                <Td {...cell.getCellProps()}>{cell.render('Cell')}</Td>
              ))}
            </Tr>
          );
        })}
      </Tbody>
    </Table>
  );
};

const App = () => {
  return (
    <ChakraProvider>
      <TableComponent />
    </ChakraProvider>
  );
};

export default App;


```
