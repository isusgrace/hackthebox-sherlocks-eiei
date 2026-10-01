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
```
### คำตอบ cryptostartup

## คำถามที่ 2 What google cloud identity is compromised? (Task 1)
```

```

## คำถามที่ 3 What IP address is the identity authenticated from? (Task 2)
```

```

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


## คำถามที่ 5 What device did the attack come from? (Task 4)
```

```

## คำถามที่ 6 What was the first failed API call made by this identity? (Task 5)
```

```

## คำถามที่ 7 What storage bucket was enumerated? (Task 6)
```

```

## คำถามที่ 8 What API call was used to exfiltrate an item from this bucket? (Task 7)
```

```

## คำถามที่ 9 Which Google Cloud command-line tool was used during the exfiltration attempt? (Task 8)
```

```

## คำถามที่ 10 What is the name of the file that was exfiltrated from the storage bucket? (Task 9)
```

```
