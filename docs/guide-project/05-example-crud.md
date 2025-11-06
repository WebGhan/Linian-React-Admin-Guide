# 增删改查示例

## 指南

接下来，我们将完成一个标准的 CRUD 业务。

### 定义类型

首先，我们要定义数据实体类型，表单类型。

目录如下：
```
├── src
│   ├── types                 # 全局类型
│   │   └── example           # 业务模块
│   │       └── template.ts   # 示例模版类型文件
```

示例模版有 id、title（标题）、description（描述）、created_at（创建时间） 和 updated_at（更新时间） 字段。

我们定义示例模版 `ExampleTemplate` 的类型：

```ts
/**
 * 示例模版
 */
type ExampleTemplate = {
    id: number;

    /** 标题 */
    title: string;

    /** 描述 */
    description: string;

    created_at: string;
    updated_at: string;
};
```

#### 表单类型

我们还需一个表单类型，用于创建和编辑：

```ts
/**
 * 示例模版表单
 */
type ExampleTemplateForm = {
    /** 标题 */
    title: string;

    /** 描述 */
    description?: string;
};
```

`description?` 中的 `?` 表示这个字段是可选的。

#### 查询参数类型

除此之外我们还需要一个查询参数类型，我们需要通过 title 字段筛选列表：

```ts
/**
 * 示例模版查询参数
 */
type ExampleTemplateQueryParams = RequestPagination & {
    /** 标题 */
    title?: string;
};
```

这里我们继承了 `RequestPagination` 类型，`RequestPagination` 是我们标准的分页参数类型。

#### 导出类型

最后，通过 `export type` 导出我们的类型：

```ts
export type { ExampleTemplate, ExampleTemplateForm, ExampleTemplateQueryParams };
```

### API 请求

### 高级表格组件 ProTable

### 处理新建

### 处理修改

### 处理删除

## 代码总览

### type

```ts title="src/types/example/template.ts"
import type { RequestPagination } from '@/types/common/requestParam.ts';

/**
 * 示例模版
 */
type ExampleTemplate = {
    id: number;

    /** 标题 */
    title: string;

    /** 描述 */
    description: string;

    created_at: string;
    updated_at: string;
};

/**
 * 示例模版表单
 */
type ExampleTemplateForm = {
    /** 标题 */
    title: string;

    /** 描述 */
    description?: string;
};

/**
 * 示例模版查询参数
 */
type ExampleTemplateQueryParams = RequestPagination & {
    /** 标题 */
    title?: string;
};

export type { ExampleTemplate, ExampleTemplateForm, ExampleTemplateQueryParams };
```

### query-fn

```ts title="src/api/query-fn/example/template.ts"
import type { ApiResponsePage } from '@/types/common/result.ts';
import type {
  ExampleTemplate,
  ExampleTemplateForm,
  ExampleTemplateQueryParams,
} from '@/types/example/template';
import { request } from '@/common/http/request.ts';

/**
 * 获取 示例模版
 */
export function getExampleTemplates(params?: ExampleTemplateQueryParams) {
  return request<ApiResponsePage<ExampleTemplate>>({
    url: '/example/example',
    method: 'GET',
    params,
  });
}

/**
 * 获取 单个示例模版
 */
export function getExampleTemplate(id: number) {
  return request<ExampleTemplate>({
    url: `/example/example/${id}`,
    method: 'GET',
  });
}

/**
 * 创建 示例模版
 */
export function createExampleTemplate(data: ExampleTemplateForm) {
  return request({
    url: '/example/example',
    method: 'POST',
    data,
  });
}

/**
 * 更新 示例模版
 */
export function updateExampleTemplate({ id, data }: { id: number; data: ExampleTemplateForm }) {
  return request({
    url: `/example/example/${id}`,
    method: 'POST',
    data,
  });
}

/**
 * 删除 示例模版
 */
export function deleteExampleTemplate(id: number) {
  return request({
    url: `/example/example/${id}/delete`,
    method: 'POST',
  });
}
```

### query-hooks

```ts title="src/api/query-hooks/example/template.ts"
import {
  createExampleTemplate,
  deleteExampleTemplate,
  getExampleTemplate,
  getExampleTemplates,
  updateExampleTemplate,
} from '@/api/query-fn/example/template.ts';
import { keepPreviousData, useMutation, useQuery, useQueryClient } from '@tanstack/react-query';
import type { ExampleTemplateQueryParams } from '@/types/example/template.ts';

/**
 * 获取 示例模版
 */
export function useExampleTemplates(params?: ExampleTemplateQueryParams) {
  return useQuery({
    queryKey: ['/template/template', params],
    queryFn: () => getExampleTemplates(params),
    select: (data) => data.data,
    placeholderData: keepPreviousData,
  });
}

/**
 * 获取 单个示例模版
 */
export function useExampleTemplate(id: number | null) {
  return useQuery({
    queryKey: [`/template/template/${id}`],
    queryFn: () => getExampleTemplate(id!),
    enabled: !!id,
    select: (data) => data.data,
  });
}

/**
 * 创建 示例模版
 */
export function useCreateExampleTemplate() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: createExampleTemplate,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['/template/template'] });
    },
  });
}

/**
 * 更新 示例模版
 */
export function useUpdateExampleTemplate() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: updateExampleTemplate,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['/template/template'] });
    },
  });
}

/**
 * 删除 示例模版
 */
export function useDeleteExampleTemplate() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: deleteExampleTemplate,
    onSuccess: (_, id) => {
      queryClient.invalidateQueries({ queryKey: ['/template/template'] });
      queryClient.removeQueries({ queryKey: [`/template/template/${id}`] });
    },
  });
}
```

### table

```tsx title="src/views/example/index.tsx"
import type { ProTableColumnsType } from '@/components/pro/ProTable/types.ts';
import ProTable, { type QueryDataParams } from '@/components/pro/ProTable';
import { type ReactNode, useRef } from 'react';
import Creator, { type CreatorRef } from '@/views/example/template/components/Creator.tsx';
import Editor, { type EditorRef } from '@/views/example/template/components/Editor.tsx';
import { Button, Dropdown, Form, Input } from 'antd';
import { PlusOutlined } from '@ant-design/icons';
import type { ExampleTemplate, ExampleTemplateQueryParams } from '@/types/example/template.ts';
import {
  useDeleteExampleTemplate,
  useExampleTemplates,
} from '@/api/query-hooks/example/template.ts';
import useCountdownConfirm from '@/components/business/confirmation/useCountdownConfirm.tsx';

function ExampleTemplateView() {
  const creatorRef = useRef<CreatorRef>(null);
  const editorRef = useRef<EditorRef>(null);
  const deleteExampleTemplate = useDeleteExampleTemplate();
  const confirmModal = useCountdownConfirm();

  function useQueryHook({ pagination, filter }: QueryDataParams<ExampleTemplateQueryParams>) {
    return useExampleTemplates({
      page: pagination?.current,
      per_page: pagination?.pageSize,
      ...filter,
    });
  }

  function handleDelete(record: ExampleTemplate) {
    confirmModal.confirm(() => {
      deleteExampleTemplate.mutate(record.id);
    });
  }

  const columns: ProTableColumnsType<ExampleTemplate> = [
    {
      title: 'ID',
      dataIndex: 'id',
      key: 'id',
      width: 80,
      hidden: true,
    },
    {
      title: '标题',
      dataIndex: 'title',
      key: 'title',
      width: 300,
    },
    {
      title: '描述',
      dataIndex: 'description',
      key: 'description',
      width: 300,
    },
    {
      title: '创建时间',
      dataIndex: 'created_at',
      key: 'created_at',
      width: 180,
    },
    {
      title: '更新时间',
      dataIndex: 'updated_at',
      key: 'updated_at',
      minWidth: 180,
    },
    {
      title: '操作',
      key: 'action',
      width: 80,
      fixed: 'right',
      render: (_, record) => (
        <Dropdown.Button
          size="small"
          trigger={['click']}
          menu={{
            style: { minWidth: '100px' },
            items: [
              {
                key: 'delete',
                onClick: () => handleDelete(record),
                label: '删除',
              },
            ],
          }}
          onClick={() => editorRef.current?.open(record.id)}
        >
          编辑
        </Dropdown.Button>
      ),
    },
  ];

  // 筛选栏
  const filterBarItems: ReactNode[] = [
    <Form.Item<ExampleTemplateQueryParams>
      name="title"
      label="标题"
    >
      <Input
        placeholder="请输入"
        allowClear
      />
    </Form.Item>,
  ];

  // 表格工具栏
  const tableToolBarItems: ReactNode = (
    <>
      <Button
        type="primary"
        icon={<PlusOutlined />}
        onClick={() => creatorRef.current?.open()}
      >
        添加
      </Button>
    </>
  );

  return (
    <>
      <ProTable<ExampleTemplate, ExampleTemplateQueryParams>
        tableTitle="示例模版"
        columns={columns}
        tableToolBarItems={tableToolBarItems}
        filterBarItems={filterBarItems}
        useQueryHook={useQueryHook}
      />

      <Creator ref={creatorRef}></Creator>
      <Editor ref={editorRef}></Editor>
    </>
  );
}

export default ExampleTemplateView;
```

### creator

```tsx title="src/views/example/template/components/Creator.tsx"
import { Button, Flex, Form, Input, Modal } from 'antd';
import { type Ref, useImperativeHandle, useState } from 'react';
import { useCreateExampleTemplate } from '@/api/query-hooks/example/template.ts';
import type { ExampleTemplateForm } from '@/types/example/template.ts';

type CreatorRef = {
  /** 打开 Modal 弹窗 */
  open: () => void;
};

type CreatorProps = {
  ref: Ref<CreatorRef>;
};

function Creator({ ref }: CreatorProps) {
  const [form] = Form.useForm();

  const [isModalOpen, setIsModalOpen] = useState<boolean>(false);
  const createExampleTemplate = useCreateExampleTemplate();

  useImperativeHandle(ref, () => {
    return {
      open() {
        setIsModalOpen(true);
      },
    };
  }, []);

  function onFinish(e: ExampleTemplateForm) {
    createExampleTemplate.mutate(e, {
      onSuccess: () => {
        form.resetFields();
        setIsModalOpen(false);
      },
    });
  }

  return (
    <Modal
      title="添加示例模版"
      width={500}
      open={isModalOpen}
      maskClosable={false}
      confirmLoading={createExampleTemplate.isPending}
      onOk={() => form.submit()}
      onCancel={() => setIsModalOpen(false)}
      footer={(_, { OkBtn, CancelBtn }) => (
        <Flex gap={8}>
          <Button
            style={{ marginRight: 'auto' }}
            onClick={() => form.resetFields()}
          >
            重置
          </Button>
          <CancelBtn />
          <OkBtn />
        </Flex>
      )}
    >
      <Form
        name="exampleTemplateCreator"
        form={form}
        layout="vertical"
        onFinish={onFinish}
        autoComplete="off"
      >
        <Form.Item<ExampleTemplateForm>
          label="标题"
          name="title"
          rules={[{ required: true, message: '请填写标题' }]}
        >
          <Input />
        </Form.Item>
        <Form.Item<ExampleTemplateForm>
          label="描述"
          name="description"
        >
          <Input />
        </Form.Item>
      </Form>
    </Modal>
  );
}

export default Creator;

export type { CreatorRef };
```

### editor

```tsx title="src/views/example/template/components/Editor.tsx"
import { type Ref, useEffect, useImperativeHandle, useState } from 'react';
import { Form, Input, Modal } from 'antd';
import {
  useExampleTemplate,
  useUpdateExampleTemplate,
} from '@/api/query-hooks/example/template.ts';
import type { ExampleTemplateForm } from '@/types/example/template.ts';

type EditorRef = {
  /** 打开 Modal 弹窗 */
  open: (id: number) => void;
};

type EditorProps = {
  ref: Ref<EditorRef>;
};

function Editor({ ref }: EditorProps) {
  const [form] = Form.useForm();

  const [isModalOpen, setIsModalOpen] = useState<boolean>(false);
  const [exampleTemplateId, setExampleTemplateId] = useState<number | null>(null);

  const { data, isFetching } = useExampleTemplate(exampleTemplateId);
  const updateUpdateExampleTemplate = useUpdateExampleTemplate();

  useImperativeHandle(ref, () => {
    return {
      open(id: number) {
        setExampleTemplateId(id);
        setIsModalOpen(true);
      },
    };
  }, []);

  useEffect(() => {
    if (data) {
      form.setFieldsValue({
        title: data.title,
        description: data.description,
      });
    }
  }, [data, form]);

  function onFinish(e: ExampleTemplateForm) {
    if (exampleTemplateId !== null) {
      updateUpdateExampleTemplate.mutate(
        { id: exampleTemplateId, data: e },
        {
          onSuccess: () => {
            form.resetFields();
            setIsModalOpen(false);
          },
        }
      );
    }
  }

  function handleReset() {
    form.resetFields();
    setExampleTemplateId(null);
  }

  return (
    <Modal
      title="编辑示例模版"
      width={500}
      open={isModalOpen}
      loading={isFetching}
      maskClosable={false}
      confirmLoading={updateUpdateExampleTemplate.isPending}
      onOk={() => form.submit()}
      onCancel={() => setIsModalOpen(false)}
      afterClose={handleReset}
    >
      <Form
        name="exampleExampleTemplateEditor"
        form={form}
        layout="vertical"
        onFinish={onFinish}
        autoComplete="off"
      >
        <Form.Item<ExampleTemplateForm>
          label="标题"
          name="title"
          rules={[{ required: true, message: '请填写标题' }]}
        >
          <Input />
        </Form.Item>
        <Form.Item<ExampleTemplateForm>
          label="描述"
          name="description"
        >
          <Input />
        </Form.Item>
      </Form>
    </Modal>
  );
}

export default Editor;

export type { EditorRef };
```
