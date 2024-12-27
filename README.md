# Python_Study24
파이썬 Ai기초 학습용

mbc아카데미 컴퓨터 교육센터 수원점에서 AI기초 학습 진행용

파이썬
https://wikidocs.net/book/1

![jump_to_python표지](https://github.com/user-attachments/assets/c6a03f99-b495-40f0-9f04-ad6f663d0ef6)


스프링 부트
https://wikidocs.net/book/7601

![junp_to_spring_boot표지](https://github.com/user-attachments/assets/f52c022e-cead-4652-9fca-5407382fe40c)


AI관련
https://wikidocs.net/book/14720
img(width:400px height:700px)

![AI와_친해지기](https://github.com/user-attachments/assets/5cf1ef94-a5be-407b-a655-61e09690733e)


Git 허브 참고자료

![캡처](https://github.com/user-attachments/assets/b3cbbb51-1a8d-4c0c-8589-04d5b18b47af)



24년 12월 20일 미션

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
2024년 12월 23일 미션 
for문도 이용해서 작성한 자판기 코드
```
# 미션
# 전에 만든 커피자판기 리스트화 해서 for문으로 구현
# 커피 종류가 5개정도 늘어나야함(커피명, 수량, 단가)
# 사용자가 커피를 반복구매
# 관리자가 판매 종류 후 통계

# 관리자 코드

while True :
    print("""관리자 전용
    1. 상품리스트
    2. 품명기입
    3. 판매시작
    4. 총 판매금액
    5. 종료
    """)


    admin_menu = input("들어 갈 곳의 메뉴의 번호를 입력하세요")
    if admin_menu == "1":

        print("상품리스트")
        for drink_Menu in drink_Menus:
            print(drink_Menu)
    elif admin_menu == "2":
        drink_Menus = []
        n = int(input("총 상품 갯수를 입력하세요: "))
        if n > 6 :
            while True:
                print("""5개 이하로 작성해주시기 바랍니다""")
                n = int(input("총 상품 갯수를 입력하세요: "))
                if n <= 6:
                    break

        for i in range(n):
            print(f"\n{i+1}번째 상품 정보를 입력하세요: ")
            drink_Name = input("음료 이름을 입력하세요: ")
            price = int(input("음료 가격을 입력하세요: "))
            drink_Count = int(input("음료 개수를 입력하세요: "))
            drink_Menus.append([drink_Name, price, drink_Count])
    elif admin_menu == "3":
          total_sale = 0
          while True :
                    print("\n[상품리스트]")
                    for i, drink in enumerate(drink_Menus):
                        print(f"{i+1}. {drink[0]} - 가격: {drink[1]}원, 수량: {drink[2]}개")
                        print("-----------")
                    custom_menu = input("음료를 선택하세요: ")
                    if custom_menu == "종료":
                        close_com=input("""종료하시겠습니까?
                        종료를 원하시면 한번 더 "종료"를 입력하세요 : """)
                        if close_com == "종료":
                          break
                    else:
                        for drink in drink_Menus:
                            if drink[0] == custom_menu or custom_menu == str(drink_Menus.index(drink) + 1):
                                selected_drink = drink
                            if not selected_drink:
                              print("존재하지 않는 음료입니다. 다시 선택해주세요.")
                              continue

                            drink_Name, price, drink_Count = selected_drink
                            if drink_Count == 0:
                                print(f"{drink_Name}은(는) 재고가 없습니다. 다른 상품을 선택해주세요.")
                                continue

                        money = int(input("금액을 넣어주세요"))
                        if money < price:
                              while True :
                                  print(("""금액이 부족합니다. %s(을)를 드시고 싶으시면 %d원을 더 넣어주시기 바랍니다.
                                            반환을 원하신다면 '반환하기'를 입력해주시기 바랍니다""" %(drink_Name,price - money)))
                                  reaction = input("금액을 추가로 넣거나 반환하기를 입력하세요: ")

                                  if reaction == "반환하기" :
                                      print("투입된 %d원을 반환합니다."%money)
                                      break      # 두번째 반복문(while)종료 첫번째로 돌아감
                                  else :
                                      try:
                                          additional_money = int(reaction)
                                          money += additional_money
                                          print("현재 투입 금액: %d원" % money)
                                          if money >= price:
                                              print("%s(을)를 받으세요." % drink_Name)
                                              drink_Count -= 1  # 음료제공
                                              total_sale += price
                                              selected_drink[2] = drink_Count   # 수량 업데이트
                                              print("잔액은 %d원입니다." % (money - price))
                                              break  # 음료 제공 후 반복문 종료
                                      except ValueError:
                                        print("유효한 금액을 입력하거나 '반환하기'를 입력하세요.")
                        elif money>= price :
                              print("%s(을)를 줍니다"% drink_Name)
                              drink_Count -= 1   # 한 잔씩 소모시킴
                              total_sale += price
                              selected_drink[2] = drink_Count   # 수량 업데이트
                              #  print("남은 %s 수량 %d 잔" % (coffee_Name, coffee_count))
                              print("잔액은 %d원 입니다"%(money - price, ))
                        else:
                              print("")
                        if drink_Count == 0 :
                              print("%s가 다 떨어졌습니다. " %drink_Name)
                              #print("현 자판기는 총 %d원을 벌었습니다"%total_sale)



    elif admin_menu == "4":
        print("총 판매금액은 %d원 입니다" %total_sale)
    elif admin_menu == "5":
        print("시스템을 종료합니다")
        break
    else:
        print("잘못된 입력입니다. 다시 입력해주세요.")

```
