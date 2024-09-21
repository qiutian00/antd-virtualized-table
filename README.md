# antd-virtualized-table

[![NPM](https://img.shields.io/npm/v/antd-virtualized-table.svg)](https://www.npmjs.com/package/antd-virtualized-table) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

`antd-virtualized-table` is a powerful library designed to enhance the performance of Ant Design tables by adding virtual scrolling capabilities. It supports infinite scrolling, tree data structures, and is especially useful when dealing with large datasets that would otherwise cause performance issues in traditional tables.

## Why Use antd-virtualized-table?

Modern web applications often need to handle large data sets efficiently. Ant Design tables can become slow and unresponsive when rendering thousands of rows. `antd-virtualized-table` addresses this problem by only rendering the rows that are visible in the viewport, significantly improving performance and user experience.

### Key Differences from Other Libraries

- **Tight Integration with Ant Design**: Seamlessly integrates with Ant Design's table component, making it easy to use without learning new table structures.
- **Tree Data Support**: Full support for tree data structures, making it ideal for complex data hierarchies.
- **Compatibility with Latest Ant Design Versions**: Supports Ant Design v4 and v5, ensuring compatibility with modern UI features.

## Installation

Ensure you have the required versions of Ant Design and React:

- **Ant Design**: v4.17.0 or above
- **React**: 16.8 or above (supports hooks)

To install `antd-virtualized-table`, run:

```bash
npm install --save antd-virtualized-table
```

Or with pnpm:

```bash
pnpm add antd-virtualized-table
```

## Prerequisites
TypeScript: Recommended if your project uses TypeScript for better type safety.
tslib: Ensure tslib is installed, as it's required for helper functions if using TypeScript.
Usage
Basic Usage
Below is a basic example demonstrating how to use antd-virtualized-table with Ant Design's table component:

```tsx
import React, { useMemo } from 'react';
import ReactDOM from 'react-dom';
import { VList } from 'antd-virtualized-table';
import { Table } from 'antd';

function Example() {
  const dataSource = [...]; // Define your data source
  const columns = [...]; // Define your table columns
  const rowKey = 'id'; // Row key to identify each row

  const vComponents = useMemo(() => {
    return VList({
      height: 1000, // Set this value to match the scrollY height
    });
  }, []);

  return (
    <Table
      dataSource={dataSource}
      columns={columns}
      rowKey={rowKey}
      scroll={{ y: 1000 }} // Scroll height, can be controlled
      components={vComponents}
    />
  );
}

ReactDOM.render(<Example />, document.getElementById('root'));
```

## Advanced Usage
antd-virtualized-table can handle various advanced scenarios such as infinite scrolling, drag and drop rows, editable cells, and more. Here are some key use cases:

Infinite Scrolling: Automatically loads more data as the user scrolls down.
Tree Table Support: Enables the use of hierarchical data within tables.
Drag and Drop: Supports reordering rows by dragging, enhancing interactivity.
Editable Cells: Integrate easily with editable tables, allowing in-place editing of cells.
Example with Infinite Scrolling

```tsx
import { useState, useMemo } from 'react';
import { Table } from 'antd';
import { VList } from 'antd-virtualized-table';

const InfiniteScrollTable = () => {
  const [data, setData] = useState(initialData);

  const loadMoreData = () => {
    // Simulate API call to fetch more data
    setData([...data, ...newData]);
  };

  const components = useMemo(() => {
    return VList({
      height: 500,
      onReachEnd: loadMoreData, // Triggered when reaching the bottom
    });
  }, [data]);

  return (
    <Table
      components={components}
      columns={columns}
      dataSource={data}
      rowKey="id"
      scroll={{ y: 500 }}
    />
  );
};
```

## API Documentation

### VList Options
- **height**: number | string (Required) - Sets the virtual scrolling height. Must match the scrollY value.

- **onReachEnd**: () => void (Optional) - Callback when the scrollbar reaches the end.

- **onScroll**: () => void (Optional) - Callback triggered during scroll events.

- **vid**: string (Optional) - Unique identifier, required when using multiple virtualized tables on the same page.

- **resetTopWhenDataChange**: boolean (Default: true) - Resets the scroll position when data changes.

### scrollTo API
The scrollTo function allows programmatic scrolling to a specific row or position within the table.

```tsx
import { scrollTo } from 'antd-virtualized-table';

// Example usage
scrollTo({
  row: 10, // Scroll to the 10th row
  y: 100,  // Y offset value
  vid: 'unique-vid', // Corresponding vid if multiple tables exist
});
```

## Examples

### Basic Examples

- [Easy Example](https://codesandbox.io/s/festive-worker-wc5wp)
- [Easy Pagination Example](https://codesandbox.io/s/gracious-resonance-tmw44)
- [Easy Resize Columns Example](https://codesandbox.io/s/vibrant-darkness-kvt56?file=/index.js)
- [Easy Infinite Load Data on Single Page](https://codesandbox.io/s/reachend-wuxianjiazaixunigundong-y9nhd)
- [Easy ScrollTo Example](https://codesandbox.io/s/scrollto-jx10t)
- [Easy Tree Table Example](https://codesandbox.io/s/reachend-wuxianjiazaixunigundong-forked-63iom?file=/src/index.tsx)

### Advanced Examples

- [Drag Row Example](https://codesandbox.io/s/drag-row-1fjg4?file=/index.js)
- [Drag Row with Handle Icon](https://codesandbox.io/s/tuozhuaishoubinglie-antd4156-forked-1d6z1?file=/index.js)
- [Editable Cell Example](https://codesandbox.io/s/editable-example-3656ln?file=/src/App.js)
- [Async Table with onListRender Example](https://codesandbox.io/s/shu-xing-biao-ge-forked-4lt6u?file=/src/index.tsx)


## Performance Tips
Limit Column Rendering: Avoid rendering complex or unnecessary columns to maintain optimal performance.
Use Memoization: Utilize useMemo or React.memo for components to minimize re-renders.
Optimize Data Fetching: Use pagination or infinite scrolling wisely to avoid fetching all data at once.
FAQ

- **1. What happens if my rows have variable heights?**
antd-virtualized-table currently calculates row height based on the first row and applies it uniformly. If rows have significantly variable heights, you might need to adjust the row height calculations manually.

- **2. How do I handle horizontal scrolling?**
The library currently supports only vertical scrolling. For horizontal scrolling, consider using other libraries in conjunction.

- **3. Why is my table not updating when data changes?**
Ensure that the resetTopWhenDataChange option is correctly configured. It defaults to true, which resets the scroll position when data changes.