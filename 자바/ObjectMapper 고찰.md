
# JAVA에서 ObjectMapper 클래스의 readValue, writeValue를 통한 JSON 형식의 데이터의 입출력 처리 예제
  
 
다음과 같은 JSON 형식의 데이터의 입출력을 해보자(첨부로 등록-Calendar.json).
- 입력 데이터 예시
-------------------------------------------------------------------------------------------- 
{"달력":[{"name":"요일","value":"월"},{"name":"요일","value":"월"},{"name":"요일","value":"수"},{"name":"요일","value":"목"},{"name":"요일","value":"금"},{"name":"요일","value":"토"},{"name":"요일","value":"일"}],"Calendar":[{"name":"Day","value":"MON"},{"name":"Day","value":"TUE"},{"name":"Day","value":"WED"},{"name":"Day","value":"THU"},{"name":"Day","value":"FRI"},{"name":"Day","value":"SAT"},{"name":"Day","value":"SUN"}]} 
-------------------------------------------------------------------------------------------- 
 
(1) FILE/URL 객체를 통한 읽기 및 콘솔 출력
 ```
public static void main(String[] args) {
 ...
   String codePath = "Calendar.json";
   loadCode(codePath);
...
 }
 
public static Map<String, Object> loadCode(String jsonFilePath) 
 { 
  ObjectMapper mapper = new ObjectMapper();
  Map<String, Object> map = null;
  try {
   // FILE 객체로 읽는 경우
   map = (Map)mapper.readValue(new File(jsonFilePath), Map.class);
   // URL 객체로 읽는 경우
   //map = (Map)mapper.readValue(new URL("http://localhost/Calendar.json"), Map.class);
   for ( String key : map.keySet() )
   {
    System.out.println("key = " + key);
    for (Iterator localIterator = ((List)map.get(key)).iterator(); localIterator.hasNext(); )
    {
     Object obj = localIterator.next();
      
     System.out.println("\tname = " + ((Map)obj).get("name").toString() + ", value = " + ((Map)obj).get("value").toString());
    }
   }
  } catch (Exception e)
  {
   System.out.println(e.toString());
  }
  return map;
 }
 ``` 
- 출력 데이터 예시
key = 달력
     name = 요일, value = 월
     name = 요일, value = 월
     name = 요일, value = 수
     name = 요일, value = 목
     name = 요일, value = 금
     name = 요일, value = 토
     name = 요일, value = 일
key = Calendar
     name = Day, value = MON
     name = Day, value = TUE
     name = Day, value = WED
     name = Day, value = THU
     name = Day, value = FRI
     name = Day, value = SAT
     name = Day, value = SUN
 
(2) FILE 객체에 출력하기
 ``` 
public static void main(String[] args) {
...
   writeJSONData();
...
}
 
public static void writeJSONData()
  {
   ObjectMapper mapper = new ObjectMapper();
   try {
   Map outerMap = new HashMap();
   
   List mapList = new ArrayList();
   Map innerMap = null;
   
   innerMap = new HashMap();
   innerMap.put("name", "Day");
   innerMap.put("value", "MON");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "Day");
   innerMap.put("value", "TUE");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "Day");
   innerMap.put("value", "WED");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "Day");
   innerMap.put("value", "THU");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "Day");
   innerMap.put("value", "FRI");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "Day");
   innerMap.put("value", "SAT");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "Day");
   innerMap.put("value", "SUN");
   mapList.add(innerMap);
   
   outerMap.put("Calendar", mapList);
   
   mapList = new ArrayList();
   
   innerMap = new HashMap();
   innerMap.put("name", "요일");
   innerMap.put("value", "월");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "요일");
   innerMap.put("value", "월");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "요일");
   innerMap.put("value", "수");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "요일");
   innerMap.put("value", "목");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "요일");
   innerMap.put("value", "금");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "요일");
   innerMap.put("value", "토");
   mapList.add(innerMap);
   
   innerMap = new HashMap();
   innerMap.put("name", "요일");
   innerMap.put("value", "일");
   mapList.add(innerMap);
   
   outerMap.put("달력", mapList);
      
   System.out.println(mapper.writeValueAsString(outerMap));
   mapper.writeValue(new File("Calendar.json"), outerMap);
   }
   catch (Exception e) 
   {
    System.out.println(e.toString());
   }
  }
  ```
