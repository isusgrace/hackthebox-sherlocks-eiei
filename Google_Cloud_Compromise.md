Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ Google_Cloud_Compromise หมวด Cloud ระดับ Medium กัน

ข้อนี้จะมีไฟล์มาให้ ชื่อ gcp.json (ต้องแตกไฟล์ก่อน)

ถ้าทำเครื่องปกติคือ กดดาวน์โหลดไฟล์ -> ใส่รหัสตามที่โจทย์ให้มา มันอยู่ในหน้าโจทย์ ให้เราคลิกเพื่อคัดลอกตรงกุญแจ

ถ้าทำใน Kali ให้ wget -O Google_Cloud_Compromise.zip "[ลิงก์]" จากนั้นมันจะถามหา password ให้ใส่ password ตามที่โจทย์ให้มา มันอยู่ในหน้าโจทย์ ให้เราคลิกเพื่อคัดลอกตรงกุญแจ

# คำถาม
## คำถามที่ 1 What’s the name of the project that was compromised? (Task 0)

```
"resource": {
      "type": "gcs_bucket",
      "labels": {
        "bucket_name": "importantbucket",
        "project_id": "cryptostartup",
        "location": "us"
      }
    }
```
สังเกตตรง project_id คำตอบจะอยู่ตรงนั้น
### คำตอบ cryptostartup

## คำถามที่ 2 What google cloud identity is compromised? (Task 1)

```
      "authenticationInfo": {
        "principalEmail": "cloud-storage-helper@cryptostartup.iam.gserviceaccount.com",
        "serviceAccountKeyName": "//iam.googleapis.com/projects/cryptostartup/serviceAccounts/cloud-storage-helper@cryptostartup.iam.gserviceaccount.com/keys/65a191ac98d4437057ff564b0093b88355e1a478"
      }
```
สังเกตตรง principalEmail คำตอบจะอยู่ตรงนั้น
### คำตอบ cloud-storage-helper@cryptostartup.iam.gserviceaccount.com

## คำถามที่ 3 What IP address is the identity authenticated from? (Task 2)
```
"requestMetadata": {
        "callerIp": "178.132.108.38",
        "callerSuppliedUserAgent": "apitools Python/3.11.3 gsutil/5.10 (darwin) analytics/disabled interactive/True command/cp google-cloud-sdk/390.0.0,gzip(gfe)",
        "requestAttributes": {
          "time": "2023-07-27T00:17:36.203631586Z",
          "auth": {}
        },
        "destinationAttributes": {}
      }
```
### คำตอบ 178.132.108.38

## คำถามที่ 4 What country does the IP originate from? (Task 3)

ขั้นตอนนี้เราจะทำใน Kali และนี่คือคำสั่งที่ใช้
```
curl -s http://ipinfo.io/178.132.108.38/json
```

- curl คือ เครื่องมือแบบ Command-line (บรรทัดคำสั่ง) ที่ใช้สำหรับถ่ายโอนข้อมูลผ่านโปรโตคอลต่างๆ เช่น HTTP, HTTPS, และอื่น ๆ 

- -s ทำหน้าที่ปิดการแสดงผล Progress Bar พวกแถบสถานะการดาวน์โหลด, ความเร็ว, เวลาที่ใช้ เพื่อให้เหลือเฉพาะข้อมูลผลลัพธ์ที่เราต้องการจริง ๆ

- ipinfo.io คือ แพลตฟอร์มที่ให้บริการเกี่ยวกับ IP Address ในส่วนนี้ทำหน้าที่ตรวจสอบและให้ข้อมูลรายละเอียดของหมายเลข IP ที่เราสนใจ

- 178.132.108.38 คือ IP ที่เราเป้าหมายของเรา

- json เป็นการระบุรูปแบบของผลลัพธ์ที่เราต้องการ โดยสั่งให้เซิร์ฟเวอร์ส่งข้อมูลกลับมาในรูปแบบ JSON
  
```
┌──(kali㉿kali)-[~/Downloads/Google_Cloud_Compromise]
└─$ curl -s http://ipinfo.io/178.132.108.38/json
{
  "ip": "178.132.108.38",
  "city": "Bucharest",
  "region": "Bucharest",
  "country": "RO",
  "loc": "44.4323,26.1063",
  "org": "AS136787 PacketHub S.A.",
  "postal": "050011",
  "timezone": "Europe/Bucharest",
  "readme": "https://ipinfo.io/missingauth"
}
```
### คำตอบ Romania

## คำถามที่ 5 What device did the attack come from? (Task 4)
```
"requestMetadata": {
        "callerIp": "178.132.108.38",
        "callerSuppliedUserAgent": "google-cloud-sdk gcloud/390.0.0 command/gcloud.projects.get-iam-policy invocation-id/a4713040dd8e4655acb6c5b4e465f403 environment/None environment-version/None interactive/True from-script/False python/3.11.3 term/xterm-256color (Macintosh; Intel Mac OS X 22.5.0),gzip(gfe)",
        "requestAttributes": {},
        "destinationAttributes": {}
      }
```
### คำตอบ Macintosh

## คำถามที่ 6 What was the first failed API call made by this identity? (Task 5)
```
{
    "protoPayload": {
      "@type": "type.googleapis.com/google.cloud.audit.AuditLog",
      "status": {
        "code": 7,
        "message": "Permission denied to enable service [compute.googleapis.com]\nHelp Token: AZZpuo5NKbSnGKgtAmsPr7UU9j9ytxoJEmA-YLVfm-trHgkHsjl3sO-NGAk7J55ckaYQFs6vHl9lNzJHo8y8C-Itw6-7aHF-aTmx5wrnbC5Zi6Hi"
      },
      "authenticationInfo": {
        "principalEmail": "cloud-storage-helper@cryptostartup.iam.gserviceaccount.com",
        "serviceAccountKeyName": "//iam.googleapis.com/projects/cryptostartup/serviceAccounts/cloud-storage-helper@cryptostartup.iam.gserviceaccount.com/keys/65a191ac98d4437057ff564b0093b88355e1a478",
        "principalSubject": "serviceAccount:cloud-storage-helper@cryptostartup.iam.gserviceaccount.com"
      },
      "requestMetadata": {
        "callerIp": "178.132.108.38",
        "callerSuppliedUserAgent": "google-cloud-sdk gcloud/390.0.0 command/gcloud.compute.firewall-rules.list invocation-id/e74de2d70ade4ce5826f68469ae37745 environment/None environment-version/None interactive/True from-script/False python/3.11.3 term/xterm-256color (Macintosh; Intel Mac OS X 22.5.0),gzip(gfe)",
        "requestAttributes": {},
        "destinationAttributes": {}
      },
      "serviceName": "serviceusage.googleapis.com",
      "methodName": "google.api.serviceusage.v1.ServiceUsage.EnableService",
      "authorizationInfo": [
        {
          "resource": "projectnumbers/421111031168/services/compute.googleapis.com",
          "permission": "serviceusage.services.enable",
          "resourceAttributes": {}
        },
        {
          "resource": "projectnumbers/421111031168/services/compute.googleapis.com",
          "permission": "serviceusage.services.enable",
          "resourceAttributes": {}
        },
        {
          "resource": "services/compute.googleapis.com",
          "permission": "servicemanagement.services.bind",
          "granted": true,
          "resourceAttributes": {}
        }
      ],
      "resourceName": "projects/421111031168/services/compute.googleapis.com",
      "request": {
        "@type": "type.googleapis.com/google.api.serviceusage.v1.EnableServiceRequest",
        "name": "projects/421111031168/services/compute.googleapis.com"
      }
    },
    "insertId": "10mka7cd1ze3",
    "resource": {
      "type": "audited_resource",
      "labels": {
        **"method": "google.api.serviceusage.v1.ServiceUsage.EnableService"**,
        "project_id": "cryptostartup",
        "service": "serviceusage.googleapis.com"
      }
    },
    "timestamp": "2023-07-27T00:16:24.221685Z",
    "severity": "ERROR",
    "logName": "projects/cryptostartup/logs/cloudaudit.googleapis.com%2Factivity",
    "receiveTimestamp": "2023-07-27T00:16:24.926595957Z"
  }
```
### คำตอบ google.api.serviceusage.v1.ServiceUsage.EnableService

## คำถามที่ 7 What storage bucket was enumerated? (Task 6)
```

```
### คำตอบ importantbucket

## คำถามที่ 8 What API call was used to exfiltrate an item from this bucket? (Task 7)
```

```
### คำตอบ storage.objects.get

## คำถามที่ 9 Which Google Cloud command-line tool was used during the exfiltration attempt? (Task 8)
```

```
### คำตอบ gsutil

## คำถามที่ 10 What is the name of the file that was exfiltrated from the storage bucket? (Task 9)
```

```
### คำตอบ secretcode.java
