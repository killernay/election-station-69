# Thailand Election Stations 2569 (2026)

ข้อมูลหน่วยเลือกตั้ง ส.ส. แบบแบ่งเขต ประจำปี พ.ศ. 2569 ในรูปแบบ JSON

## ที่มาของข้อมูล

ข้อมูลนี้ถูกรวบรวมจากหลายแหล่ง:

### 1. ข้อมูลหน่วยเลือกตั้ง
- **แหล่งที่มา:** ฐานข้อมูล ERS2026 (Election Reporting System)
- **ต้นทาง:** คณะกรรมการการเลือกตั้ง (กกต.)
- **ข้อมูล:** รหัสหน่วย, ชื่อสถานที่, อำเภอ, ตำบล, จำนวนผู้มีสิทธิ

### 2. ข้อมูลพิกัด (Geolocation)
- **แหล่งที่มา:** [PPLEThai/election-station-66](https://github.com/PPLEThai/election-station-66)
- **วิธีการ:** ใช้ **Fuzzy String Matching** จับคู่ชื่อหน่วยเลือกตั้งจาก กกต. ปี 2569 กับข้อมูลพิกัดจากปี 2566
- **ข้อจำกัด:** เนื่องจากชื่อหน่วยเลือกตั้งระหว่างสองปีมีความคล้ายคลึงแต่ไม่เหมือนกันทั้งหมด (เช่น ชื่อสถานที่เปลี่ยน, พิมพ์ต่างกัน) การจับคู่อาจมีข้อผิดพลาดได้

> **คำเตือน:** พิกัด lat/long อาจไม่ถูกต้อง 100% เนื่องจากเป็นการ fuzzy match จากข้อมูลปี 2566 กรุณาตรวจสอบก่อนนำไปใช้งานที่ต้องการความแม่นยำสูง

## สถิติข้อมูล

- **จำนวนหน่วยเลือกตั้ง:** 94,441 หน่วย
- **จำนวนจังหวัด:** 77 จังหวัด
- **จำนวนเขตเลือกตั้ง:** 400 เขต
- **จำนวนผู้มีสิทธิเลือกตั้ง:** 52,922,923 คน
- **ปีที่ใช้:** พ.ศ. 2569

## โครงสร้างข้อมูล

```json
{
  "version": "2569",
  "type": "election_stations",
  "description": "หน่วยเลือกตั้ง ส.ส. แบบแบ่งเขต พ.ศ. 2569",
  "total_stations": 94441,
  "total_provinces": 77,
  "total_areas": 400,
  "generated_at": "2026-01-22",
  "provinces": [...]
}
```

### รายละเอียด Fields

| Field | Type | Description |
|-------|------|-------------|
| `version` | string | ปี พ.ศ. ของข้อมูล |
| `type` | string | ประเภทข้อมูล (`election_stations` = หน่วยเลือกตั้ง) |
| `description` | string | คำอธิบายชุดข้อมูล |
| `total_stations` | number | จำนวนหน่วยเลือกตั้งทั้งหมด |
| `total_provinces` | number | จำนวนจังหวัดทั้งหมด (77 จังหวัด) |
| `total_areas` | number | จำนวนเขตเลือกตั้งทั้งหมด (400 เขต) |
| `generated_at` | string | วันที่สร้างข้อมูล |
| `provinces` | array | รายการจังหวัดทั้งหมด |

### โครงสร้าง Province

```json
{
  "name": "กรุงเทพมหานคร",
  "code": "10",
  "region": "central",
  "total_areas": 33,
  "total_stations": 6916,
  "areas": [...]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | ชื่อจังหวัด |
| `code` | string | รหัสจังหวัด (2 หลัก) |
| `region` | string | ภาค (`central`, `north`, `northeast`, `south`, `east`, `west`) |
| `total_areas` | number | จำนวนเขตเลือกตั้งในจังหวัด |
| `total_stations` | number | จำนวนหน่วยเลือกตั้งในจังหวัด |
| `areas` | array | รายการเขตเลือกตั้ง |

### โครงสร้าง Area (เขตเลือกตั้ง)

```json
{
  "area": 1,
  "name": "กรุงเทพมหานคร เขต 1",
  "total_stations": 215,
  "eligible_voters": 130423,
  "stations": [...]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `area` | number | หมายเลขเขตเลือกตั้ง |
| `name` | string | ชื่อเขตเลือกตั้ง |
| `total_stations` | number | จำนวนหน่วยเลือกตั้งในเขต |
| `eligible_voters` | number | จำนวนผู้มีสิทธิเลือกตั้งในเขต |
| `stations` | array | รายการหน่วยเลือกตั้ง |

### โครงสร้าง Station (หน่วยเลือกตั้ง)

```json
{
  "code": "81-01-810101-001",
  "name": "หอประชุมวิทยาลัยสารพัดช่างกระบี่",
  "district": "เมืองกระบี่",
  "subdistrict": "ปากน้ำ",
  "lat": 8.0863,
  "lng": 98.9063
}
```

| Field | Type | Description |
|-------|------|-------------|
| `code` | string | รหัสหน่วยเลือกตั้ง (รูปแบบ: `XX-YY-ZZZZZZ-NNN`) |
| `name` | string | ชื่อสถานที่ตั้งหน่วยเลือกตั้ง |
| `district` | string | ชื่ออำเภอ/เขต |
| `subdistrict` | string | ชื่อตำบล/แขวง |
| `lat` | number | ละติจูด (fuzzy matched จาก election-station-66, อาจเป็น null) |
| `lng` | number | ลองจิจูด (fuzzy matched จาก election-station-66, อาจเป็น null) |

> **Tip:** หมายเลขหน่วยเลือกตั้ง = เลข 3 หลักสุดท้ายของ `code` (เช่น `81-01-810101-001` → หน่วยที่ **1** ของตำบลปากน้ำ)

## การใช้งาน

### JavaScript / Node.js

```javascript
// อ่านไฟล์
const data = require('./election-stations-2569.json');

// หาหน่วยเลือกตั้งของจังหวัด
const bangkok = data.provinces.find(p => p.name === 'กรุงเทพมหานคร');
console.log(`กรุงเทพมหานครมี ${bangkok.total_stations} หน่วยเลือกตั้ง`);

// หาหน่วยเลือกตั้งจากรหัส
function findStation(stationCode) {
  for (const province of data.provinces) {
    for (const area of province.areas) {
      const station = area.stations.find(s => s.code === stationCode);
      if (station) {
        return {
          province: province.name,
          area: area.area,
          areaName: area.name,
          ...station
        };
      }
    }
  }
  return null;
}

console.log(findStation('10-01-100101-001'));
```

### Python

```python
import json

# อ่านไฟล์
with open('election-stations-2569.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

# หาหน่วยเลือกตั้งของจังหวัด
bangkok = next((p for p in data['provinces'] if p['name'] == 'กรุงเทพมหานคร'), None)
print(f"กรุงเทพมหานครมี {bangkok['total_stations']} หน่วยเลือกตั้ง")

# หาหน่วยเลือกตั้งจากรหัส
def find_station(station_code):
    for province in data['provinces']:
        for area in province['areas']:
            for station in area['stations']:
                if station['code'] == station_code:
                    return {
                        'province': province['name'],
                        'area': area['area'],
                        'area_name': area['name'],
                        **station
                    }
    return None

print(find_station('10-01-100101-001'))
```

### cURL / Fetch (ถ้า host บน GitHub)

```bash
curl -s https://raw.githubusercontent.com/killernay/election-station-69/main/election-stations-2569.json | jq '.provinces[0]'
```

```javascript
fetch('https://raw.githubusercontent.com/killernay/election-station-69/main/election-stations-2569.json')
  .then(res => res.json())
  .then(data => console.log(data.total_stations));
```

## รูปแบบรหัสหน่วยเลือกตั้ง

รหัสหน่วยเลือกตั้งมีรูปแบบ: `XX-YY-ZZZZZZ-NNN`

| ส่วน | ความหมาย | ตัวอย่าง |
|------|----------|---------|
| `XX` | รหัสจังหวัด | 10 = กรุงเทพมหานคร, 81 = กระบี่ |
| `YY` | เขตเลือกตั้ง | 01 = เขตเลือกตั้งที่ 1 |
| `ZZZZZZ` | รหัสตำบล/แขวง | 810101 = รหัสตำบลจากกรมการปกครอง |
| `NNN` | **หมายเลขหน่วยในตำบล** | 001 = หน่วยที่ 1 ของตำบลนั้น |

### หมายเลขหน่วยเลือกตั้ง (NNN)

**สำคัญ:** หมายเลขหน่วย (NNN) จะ **ขึ้นใหม่จาก 001** เมื่อเปลี่ยนตำบล ไม่ใช่นับต่อเนื่องทั้งเขต

**ตัวอย่าง:** กระบี่ เขต 1

| รหัส | ตำบล | หน่วยที่ |
|------|------|---------|
| `81-01-810101-001` | ปากน้ำ | หน่วยที่ 1 |
| `81-01-810101-002` | ปากน้ำ | หน่วยที่ 2 |
| `81-01-810101-019` | ปากน้ำ | หน่วยที่ 19 |
| `81-01-810103-001` | กระบี่น้อย | หน่วยที่ 1 ← **ขึ้นใหม่** |
| `81-01-810103-002` | กระบี่น้อย | หน่วยที่ 2 |
| `81-01-810803-001` | คลองขนาน | หน่วยที่ 1 ← **ขึ้นใหม่** |

ดังนั้น ถ้าต้องการทราบว่าเป็น "หน่วยที่เท่าไหร่" ให้ดูจาก **เลข 3 หลักสุดท้าย** ของ code (NNN) ซึ่งจะเป็นหมายเลขหน่วยภายในตำบลนั้นๆ

## ข้อมูลที่เกี่ยวข้อง

- [election-area-69](https://github.com/killernay/election-area-69) - ข้อมูลเขตเลือกตั้ง ส.ส. แบบแบ่งเขต พ.ศ. 2569
- [PPLEThai/election-station-66](https://github.com/PPLEThai/election-station-66) - ข้อมูลหน่วยเลือกตั้งปี 2566 พร้อมพิกัด (ต้นทางข้อมูล lat/long)

## Credits

ขอขอบคุณ [PPLEThai](https://github.com/PPLEThai) สำหรับข้อมูลพิกัดหน่วยเลือกตั้งจากปี 2566 ที่นำมาใช้ในการ fuzzy match กับข้อมูลปี 2569

## License

ข้อมูลนี้เป็นข้อมูลสาธารณะจากคณะกรรมการการเลือกตั้ง (กกต.) เผยแพร่เพื่อประโยชน์สาธารณะ

## Disclaimer

ข้อมูลนี้จัดทำขึ้นจากฐานข้อมูล ERS2026 ซึ่งรวบรวมข้อมูลจาก กกต. และพิกัด lat/long จาก PPLEThai/election-station-66 ผ่านการ fuzzy matching

**ข้อควรระวัง:**
- ข้อมูลหน่วยเลือกตั้งอาจมีการเปลี่ยนแปลงจาก กกต.
- **พิกัด lat/long อาจไม่ถูกต้อง** เนื่องจากเป็นการจับคู่ชื่อสถานที่ที่คล้ายกันแต่ไม่เหมือนกันทั้งหมด (ชื่อเปลี่ยน, สะกดต่างกัน, หน่วยใหม่)
- บางหน่วยอาจไม่มีพิกัด (null) หากไม่พบการจับคู่ที่เหมาะสม

**ผู้จัดทำไม่รับประกันความถูกต้องสมบูรณ์ของข้อมูล และไม่รับผิดชอบต่อความเสียหายใดๆ ที่อาจเกิดขึ้นจากการใช้ข้อมูลนี้** หากต้องการข้อมูลที่ถูกต้องสมบูรณ์ กรุณาตรวจสอบกับเอกสารต้นฉบับจากคณะกรรมการการเลือกตั้ง

---

Generated from ERS2026 Database
