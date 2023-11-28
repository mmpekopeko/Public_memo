```tsx

import { useTable } from '@tanstack/react-table';
import { Box, ChakraProvider, CSSReset, extendTheme, Table, Tbody, Td, Th, Thead, Tr } from '@chakra-ui/react';
import React from 'react';

// ダミーデータ
const dataList = [
  { id: 1, name: 'John Doe', age: 25 },
  { id: 2, name: 'Jane Doe', age: 30 },
  { id: 3, name: 'Bob Smith', age: 22 },
];

// Chakra UIのテーマ
const theme = extendTheme({});

// Reactコンポーネント
const App = () => {
  // テーブルのカラムとデータを設定
  const { getTableProps, getTableBodyProps, headerGroups, rows, prepareRow } = useTable({ columns, data: dataList });

  return (
    <ChakraProvider theme={theme}>
      <Box p={4}>
        <Table {...getTableProps()} width="100%">
          <Thead>
            {headerGroups.map(headerGroup => (
              <Tr {...headerGroup.getHeaderGroupProps()}>
                {headerGroup.headers.map(column => (
                  <Th {...column.getHeaderProps()}>{column.render('Header')}</Th>
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
      </Box>
    </ChakraProvider>
  );
};

// テーブルのカラム定義
const columns = [
  { Header: 'ID', accessor: 'id' },
  { Header: 'Name', accessor: 'name' },
  { Header: 'Age', accessor: 'age' },
];

export default App;

```
