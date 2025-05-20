# 🪓 Root Check

The **Malloc Security SDK** offers a comprehensive root detection feature that checks for common indicators of a rooted device. This includes known rooting binaries, packages, superuser access, and modified security properties.

> This operation is available in both synchronous and asynchronous versions (with callbacks).

---

## ✅ Asynchronous Usage (Recommended)

####  Java
```java
MallocSDK.rootCheckAsync(new MallocSDK.ScanFinishedCallback() {
    @Override
    public void onScanFinished(JSONObject rootCheckResults) {
        // Use the rootCheckResults
    }
});
```

---

## ⚡ Synchronous Usage

> Do **not** call this on the main/UI thread.

####  Java
```java
ExecutorService executor = Executors.newSingleThreadExecutor();
executor.execute(new Runnable() {
    @Override
    public void run() {
        JSONObject rootCheckResults = MallocSDK.rootCheckSync();
        // Use the rootCheckResults
    }
});
executor.shutdown();
```

---

## 📦 Sample JSON Response

```json
{
  "status": "success",
  "details": {
    "rooted_flag": false,
    "root_check_results": [
      {
        "issue_found": false,
        "check_description": "Check for Device Rooting Apps"
      },
      {
        "issue_found": false,
        "check_description": "Check for Rooting Binaries"
      },
      {
        "issue_found": false,
        "check_description": "Check Improperly Released Packages"
      },
      {
        "issue_found": false,
        "check_description": "Check for Development Packages"
      },
      {
        "issue_found": false,
        "check_description": "Detect Development Keys"
      },
      {
        "issue_found": false,
        "check_description": "Check for Dangerous Apps"
      },
      {
        "issue_found": false,
        "check_description": "Check Device Security Properties"
      },
      {
        "issue_found": false,
        "check_description": "Check Superuser Access"
      },
      {
        "issue_found": false,
        "check_description": "Check for Superuser APK"
      },
      {
        "issue_found": false,
        "check_description": "Check for Superuser binary"
      },
      {
        "issue_found": false,
        "check_description": "Check for embedded OS"
      },
      {
        "issue_found": false,
        "check_description": "Check for rooting frameworks"
      },
      {
        "issue_found": false,
        "check_description": "Check for reset device fingerprint properties"
      },
      {
        "issue_found": false,
        "check_description": "Paths that should be read-only"
      },
      {
        "issue_found": false,
        "check_description": "Check for Man In the Middle Hooks"
      }
    ]
  }
}
```

---

## 🧠 Notes

- `rooted_flag`: A high-level boolean flag indicating if the device appears to be rooted.
- `root_check_results`: A list of all individual root checks performed, with their respective results and descriptions.
- If `rooted_flag` is `true`, your app may choose to restrict certain actions or warn the user.

---

## 🔒 Best Practices

- Always perform root checks **after SDK initialization** is completed.
- Use the **asynchronous** version for better UI performance.
