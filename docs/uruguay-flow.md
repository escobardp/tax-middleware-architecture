# Electronic Invoice Flow – Uruguay (DGI via CTC)

## Overview

Este flujo describe el proceso de emisión de factura electrónica desde SAP hacia la DGI (Uruguay), utilizando un proveedor intermediario (CTC – Uruware).

A diferencia de otros países, la comunicación no es directa con el organismo fiscal, sino a través de un proveedor autorizado.

---

## Step-by-Step Flow

1. **Invoice Creation (SAP ERP)**  
   Se genera una factura en SAP, activando el proceso de integración.

2. **Data Extraction (Middleware)**  
   El middleware recibe los datos relevantes de la factura.

3. **Transformation**  
   Los datos se transforman al formato requerido por el proveedor CTC (Uruware).

4. **Validation**  
   Validaciones fiscales:
   - RUT válido  
   - Tipo de comprobante  
   - Reglas de DGI  

5. **Routing**  
   El middleware identifica que el destino es Uruguay y deriva al **Adapter Uruguay**.

6. **Adapter Processing**  
   El adapter prepara la request específica para el proveedor CTC.

7. **Communication with CTC Provider (Uruware)**  
   Se envía la factura al proveedor, que actúa como intermediario.

8. **CTC Processing**  
   Uruware:
   - Valida el documento  
   - Lo adapta a formato requerido por DGI  
   - Lo envía al organismo fiscal  

9. **DGI Response**  
   La DGI responde al proveedor con:
   - Aprobación  
   - Rechazo  

10. **Response Propagation**  
    El proveedor retorna la respuesta al middleware.

11. **Logging & Monitoring**  
    Registro completo de la transacción.

12. **Error Handling**  
    Manejo de errores en múltiples niveles:
    - Middleware  
    - Proveedor  
    - DGI  

---

## Key Differences vs Direct Integration

- Intermediación obligatoria (CTC)  
- Mayor latencia en respuesta  
- Dependencia de proveedor externo  
- Mayor complejidad en debugging  

---

## Key Considerations

- Gestión de timeouts y reintentos  
- Trazabilidad end-to-end (SAP → CTC → DGI)  
- Manejo de estados intermedios  
- Versionado de formatos  

---

## Outcome

- Factura validada por DGI vía proveedor  
- Cumplimiento normativo  
- Integración desacoplada y escalable
