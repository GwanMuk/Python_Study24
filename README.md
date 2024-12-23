# Pytion_Study24
파이썬 Ai기초 학습용

mbc아카데미 컴퓨터 교육센터 수원점에서 AI기초 학습 진행용

파이썬
https://wikidocs.net/book/1

스프링 부트
https://wikidocs.net/book/7601

AI관련
https://wikidocs.net/book/14720


```
# 미션
# 관리자가 커피가격과 커피명을 정하고 개수를 입력한다
# 소비자가 커피를 구매하는데 잔돈 나와야 함
# 판매 종료 후 관리자가 커피 판매한 총액을 파악해야 함

# 관리자 설정

coffee_Name = input("음료 이름을 입력하세요: ")
price = int(input("음료 가격을 입력하세요: "))
coffee_count = int(input("음료 개수를 입력하세요: "))

total_sale = price * coffee_count

while True :
      money = int(input("금액을 넣어주세요"))
      if money < price:
          while True :
              print(("""금액이 부족합니다. %s(을)를 드시고 싶으시면 %d원을 더 넣어주시기 바랍니다.
                        반환을 원하신다면 '반환하기'를 입력해주시기 바랍니다""" %(coffee_Name,price - money)))
              reaction = input("금액을 추가로 넣거나 반환하기를 입력하세요: ")

              if reaction == "반환하기" :
                  print("금액 %d원을 반환합니다."%money)
                  break      # 두번째 반복문(while)종료 첫번째로 돌아감
              else :
                  try:
                      additional_money = int(reaction)
                      money += additional_money
                      print("현재 투입 금액: %d원" % money)
                      if money >= price:
                          print("%s(을)를 줍니다." % coffee_Name)
                          coffee_count -= 1  # 음료제공
                          print("잔액은 %d원입니다." % (money - price))
                          break  # 음료 제공 후 반복문 종료
                  except ValueError:
                      print("유효한 금액을 입력하거나 '반환하기'를 입력하세요.")
      elif money>= price :
          print("%s(을)를 줍니다"% coffee_Name)
          coffee_count = coffee_count - 1   # 한 잔씩 소모시킴
          #  print("남은 %s 수량 %d 잔" % (coffee_Name, coffee_count))
          print("잔액은 %d원 입니다"%(money - price, ))
      else:
          print("")
      if coffee_count == 0 :
          print("%s가 다 떨어졌습니다. 판매를 중지합니다" %coffee_Name)
          print("현 자판기는 총 %d원을 벌었습니다"%total_sale)
          break

```
