
```tsx
import React from 'react';
import { useTable } from '@tanstack/react-table';
import { ChakraProvider, Table, Thead, Tbody, Tr, Th, Td, Box } from '@chakra-ui/react';

const TableExample = () => {
  // 列の定義
  const columns = React.useMemo(
    () => [
      { Header: 'ID', accessor: 'id' },
      { Header: '名前', accessor: 'name' },
      { Header: 'サイズ', accessor: 'size' },
      { Header: '個数', accessor: 'count' },
    ],
    []
  );

  // useTableのインスタンスを作成し、テーブルのプロパティを取得
  const {
    getTableProps,
    getTableBodyProps,
    headerGroups,
    rows,
    prepareRow,
  } = useTable({ columns, data: list });

  return (
    <Box>
      <Table {...getTableProps()}>
        <Thead>
          {headerGroups.map((headerGroup) => (
            <Tr {...headerGroup.getHeaderGroupProps()}>
              {headerGroup.headers.map((column) => (
                <Th {...column.getHeaderProps()}>{column.render('Header')}</Th>
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
                  <Td {...cell.getCellProps()}>{cell.render('Cell')}</Td>
                ))}
              </Tr>
            );
          })}
        </Tbody>
      </Table>
    </Box>
  );
};

const App = () => {
  return (
    <ChakraProvider>
      <TableExample />
    </ChakraProvider>
  );
};

export default App;

```
