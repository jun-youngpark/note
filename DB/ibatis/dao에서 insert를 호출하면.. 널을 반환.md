# ibatis 사용시 dao에서 insert를 호출하면.. 널을 반환합니다. -_-;
 
아래와 같이
 public boolean addBizRelReviewInfo(BizRelReviewInfo bizRelReviewInfo) {
  Integer nResult  = 0;
  try {
   nResult = (Integer) getSqlMapClientTemplate().insert(
     "BizResPlanApplySQL.addBizRelReviewInfo", bizRelReviewInfo);
  
  } catch (Exception e) {
   e.printStackTrace();
   return false;
  }
  return nResult > 0;
 }
 
insert로 호출할 경우.. insert가 제대로 되어도 기본적으로 널을 반환합니다.
 
이것을 해결하기 위해 2가지 방법이 있습니다.
 
 
1. 퀴리에서 selectKey 태그를 이용해서 아무값이나 하나 반환하게 하는 방법.
 <insert id="addBizRelReviewInfo" parameterClass="BizRelReviewInfo">
  INSERT INTO TN_WA_REL_REVIEW
  (
   INBPN_CODE,
   NOTI_SEQ, 
   XXXX ...
  ) VALUES (
   #ibnpnCode#,
   #notiSeq#
    XXXX...
  )
       <selectKey keyProperty="notiSeq" resultClass="int">
      SELECT 1 as maxcount FROM dual
       </selectKey>  
   </insert>
 
2. dao 에서 insert 대신 update로 호출하는 방법.
public boolean addBizRelReviewInfo(BizRelReviewInfo bizRelReviewInfo) {
  Integer nResult  = 0;
  try {
   nResult = (Integer) getSqlMapClientTemplate().update(
     "BizResPlanApplySQL.addBizRelReviewInfo", bizRelReviewInfo);
  
  } catch (Exception e) {
   e.printStackTrace();
   return false;
  }
  return nResult > 0;
 }
 
참고하세요~~
