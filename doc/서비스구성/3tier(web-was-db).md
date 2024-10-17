### WEB[관리자화면/사용자화면] -> WAS[마이크로서비스] -> DB


graph TD
    A[Client]
    B[Web Server]
    C[Application Server]
    D[Database]

    subgraph Web
        direction TB
        E[일반 사용자 페이지]
        F[관리자 페이지]
    end

    A --> B
    B --> E
    B --> F
    E --> C
    F --> C
    C --> D

[![](https://mermaid.ink/img/pako:eNptkE1qwzAQRq8itE4u4EXBvxdIoAs5i7E1iQW2bGSpUEIg9ACly1BIly2FLLrIsidq1DtUsVySQmel977RDMyali1HGtCVgq4i8ySXxFXI4lqg1AuPEbvFgsxQ3aEaVczCrqtFCVq08m-UsAQ0FNCjE171pvAL3BxvzsWFwnL4P48uNmV2_3n62BH7cLDP7_bliXw_7uz-aN-2i0tbxr6O29Pr4b8cJf_dHJLp9IaM46MB0mvIPKQDxB6ya4gHSOiENqgaENwda32OcqorbDCngXtyXIKpdU5zuXGtYHQ7u5clDbQyOKGqNauKBkuoe0em46AxEeBu0ox28wNvr4QF?type=png)](https://mermaid.live/edit#pako:eNptkE1qwzAQRq8itE4u4EXBvxdIoAs5i7E1iQW2bGSpUEIg9ACly1BIly2FLLrIsidq1DtUsVySQmel977RDMyali1HGtCVgq4i8ySXxFXI4lqg1AuPEbvFgsxQ3aEaVczCrqtFCVq08m-UsAQ0FNCjE171pvAL3BxvzsWFwnL4P48uNmV2_3n62BH7cLDP7_bliXw_7uz-aN-2i0tbxr6O29Pr4b8cJf_dHJLp9IaM46MB0mvIPKQDxB6ya4gHSOiENqgaENwda32OcqorbDCngXtyXIKpdU5zuXGtYHQ7u5clDbQyOKGqNauKBkuoe0em46AxEeBu0ox28wNvr4QF)
