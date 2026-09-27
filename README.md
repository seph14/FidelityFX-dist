# FidelityFX SDK (ffx_api) — vendored subset

Provenance: FidelityFX SDK **v2.3.0** (FSR SDK "Redstone"), MIT license,
https://github.com/GPUOpen-LibrariesAndSDKs/FidelityFX-SDK (tag v2.3.0),
runtime DLLs extracted from the release asset `FidelityFX-Samples-v2.3.0-prebuilt.zip`.

Contents (only what the FSR 3.1 upscaler backend needs):

- `include/ffx_api/` — public C headers:
  - `ffx_api.h` / `ffx_api_types.h` (core + types)
  - `ffx_upscale.h` (upscale create/dispatch descs; the two `../../api/include/…`
    include lines were rewritten to point at the sibling headers)
  - `dx12/ffx_api_dx12.h` (DX12 backend desc + `ffxApiGetResourceDX12` helper)
- `bin/` — runtime DLLs (loaded dynamically by the engine, never linked):
  - `amd_fidelityfx_loader_dx12.dll` — exports `ffxCreateContext/ffxDestroyContext/ffxConfigure/ffxQuery/ffxDispatch`
  - `amd_fidelityfx_upscaler_dx12.dll` — FSR 3.1/FSR 4 upscaler provider; must sit
    next to the loader DLL (the loader discovers it by name)

Both DLLs must be deployed next to the engine executable (post-build copy).
