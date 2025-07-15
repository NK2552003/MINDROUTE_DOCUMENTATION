# MindRoute Feature Flowchart

The diagram below illustrates how the MindRoute feature flows through the application, using the folder structure to map each logical step.

```mermaid
flowchart TD
  subgraph AppLayer
    A["app/layout.tsx\n(Global layout)"] --> B["app/provider.tsx\n(Context provider)"]
    B --> C["app/page.tsx\n(Homepage)"]
    B --> D["app/(routes)\n(Route group)"]
  end

  subgraph RouteHandlers
    D --> E["app/(routes)/search/[libid]/page.tsx\n(Search results)"]
    D --> F["app/(routes)/roadmap/[libid]/page.tsx\n(Roadmap detail)"]
  end

  subgraph UIComponents
    E --> G["app/(routes)/search/_components/cardComponent.tsx\n(Result cards)"]
    F --> H["app/(routes)/roadmap/_components/CustomNode.tsx\n(Graph nodes)"]
    F --> I["app/(routes)/roadmap/_components/Header.tsx\n(Page header)"]
  end

  subgraph DataServices
    G & H & I --> J["components/utils/supabase.tsx\n(Supabase client)"]
  end

  subgraph APIEndpoints
    J --> K["api/roadmap/route.ts\n(Fetch roadmap data)"]
    J --> L["api/generate-hierarchy-json/route.ts\n(Build hierarchy JSON)"]
  end

  subgraph BackgroundProcessing
    K & L --> M["inngest/functions.ts\n(Background jobs)"]
    M --> J
  end

  classDef app fill:#E8F0FE,stroke:#4285F4;
  classDef routes fill:#E8FDF3,stroke:#34A853;
  classDef ui fill:#FFF7E6,stroke:#FBBC05;
  classDef services fill:#FCE8E6,stroke:#EA4335;
  classDef api fill:#F3E8FF,stroke:#9338E3;
  classDef jobs fill:#E8F5FE,stroke:#4285F4;

  class A,B,C,D app;
  class E,F routes;
  class G,H,I ui;
  class J services;
  class K,L api;
  class M jobs;
```

This flowchart shows:

1. **App Layer**: The root `app/` folder bootstraps the layout and context provider.
2. **Route Handlers**: Dynamic pages under `app/(routes)` handle search and roadmap views.
3. **UI Components**: Each page imports presentational components from the `_components` folders.
4. **Data Services**: Shared `supabase.tsx` provides the client for database queries.
5. **API Endpoints**: Next.js route files under `api/` fetch or generate required data.
6. **Background Processing**: Inngest jobs handle long-running tasks and feed results back into the system.
