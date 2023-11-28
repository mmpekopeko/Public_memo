
```
useTable, SortingState

useTableの書き方は古い、SortingStateのところだけ参考にする

```

```tsx

import * as React from 'react';
import { useTable, SortingState } from 'react-table';
import { ChakraProvider, Table, Tbody, Td, Th, Thead, Tr } from '@chakra-ui/react';

// テーブルのカラム定義
const columns = [
  { Header: 'ID', accessor: 'id' },
  { Header: '名前', accessor: 'name' },
  { Header: 'サイズ', accessor: 'size' },
  { Header: '数量', accessor: 'count' },
];

const App = () => {
  // テーブルのインスタンスを生成
  const {
    getTableProps,
    getTableBodyProps,
    headerGroups,
    rows,
    prepareRow,
    state: { sorting }, // ソート状態を取得
  } = useTable(
    {
      columns,
      data: list,
      initialState: {
        sorting: [
          // 初期ソート設定（名前で昇順）
          { id: 'name', desc: false },
        ],
      },
    },
    SortingState
  );

  return (
    <ChakraProvider>
      <Table {...getTableProps()}>
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
    </ChakraProvider>
  );
};

export default App;

```
