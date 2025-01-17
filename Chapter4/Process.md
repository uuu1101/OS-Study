 ## Process 
 
 OS는 사용자에게 프로세스를 제공 
 프로세스의 비공식 정의: 실행 중인 프로그램
 
 Virtualizing(가상화)을 통해서 CPU가 여러개 존재하는 것처럼 만든다.
 한 프로세스를 실행한 다음 중지하고 다른 프로세스를 실행하는 등의 작업을 수행하면
 실제로 물리적 CPU가 1개 밖에 없을 때 많은 가상의 CPU가 존재하는 것처럼 보일 수 있다.
 
 Time Sharing(시분할)이라는 기법을 통해서 사용자가 원하는 만큼 동시에 프로세스를 실행할 수 있게 한다.
이 기법은 CPU를 공유하기 때문에 각 프로세스의 성능은 낮아진다.

효율적인 가상화를 구현하기위해서는 low-level machinery 와 high-level intelligence가 필요하다.
low-level machinery를 mechanisms 라고하며 이 mechanisms은 기능 개발을 위한 조각(?) 저수준 함수 또는 저수준 프로토콜를 뜻한다.
high-level intelligence는 정책(policy)라고 하며 이 정책은 OS에서 어떤 결정을 내리는데 사용되는 알고리즘이다.

1. 프로세스 개념 
프로세스는 실행중인 프로그램 
프로세스의 구성요소를 이해하기 위해서는 machine State(하드웨어 상태)를 이해해야한다.
machine State? 프로그램이 실행중일때 읽거나 업데이트 할 수 있는 것
프로세스의 하드웨어 상태 중 가장 중요한 구성 요소는 메모리다.
실행 중인 프로그램이 읽고 쓰는 데이터는 메모리에 적재된다.

레지스터도 프로세스의 하드웨어 상태를 구성하는 요소 중 하나이다.
특별한 레지스터들이 존재하는데, program counter(PC)가 있고, instruction pointer or IP라고도 불린다.
stack Pointer 와 frame Pointer가 있고 이들은 지역변수 그리고 리턴 주소값을 관리한다.

2. 프로세스 API
- Create: shell에 command를 입력하거나 더블클릭을 통해서 생성가능하다.
- Destroy: 대부분의 프로세스는 완료되면 스스로 종료된다. 만약 그러지 않는다면 user가 kill 해야한다.
- Wait: 어떤 프로세스의 중지를 기다린다.
- Miscellaneous Control: 제거, 대기 이외의 여러 가지 제어
- State: 프로세스의 상태정보를 얻어냄, 얼마동안 실행 되었는지 등등 어떤상태에 있었는지 등

3. 프로세스 생성에 대해 더 자세하게
프로그램이 어떻게 프로세스로 변형이 되나?
프로그램 실행을 위해서 OS가 하는 첫번째 작업은 프로그램 코드와 정적데이터를 메모리, 프로세스의 주소공간에 load하는 것이다.
프로그램은 디스크 또는 SSD(flash 기반)에 실행가능한 형식으로 존재한다. 초기 운영체제는 모든부분의 코드와 데이터를 메모리에 load하였다.
현재의 운영체제들은 프로그램을 실행하면서 필요한 부분만 메모리에 탑재한다. 코드와 데이터의 lazy loading에 대해서 이해하려면 Paging, Swapping에 대한 이해가 필요하다.
코드와 정적 데이터가 메모리로 load된 후 프로세스를 실행시키기 전에 특정 크기의 메모리 공간이 프로그램의 run-time stack(or just Stack)용도로 할당되어야 한다.

즉, 코드와 정적 데이터를 메모리에 탑재하고, 스택과 힙을 생성하고 초기화하고, 입출력 셋업과 관계된 다른 작업들을 마치게 되면
운영체제는 프로그램 실행을 위한 준비를 마치게 된다.

4. 프로세스 상태
- Running: 실행 상테에서 프로세스는 프로세서에서 실행중이다.
- Ready: 준비 상태에서는 프로세스는 실행할 준비가 되어 있지만, 여러 이유로 대기중인 상태(다른 프로세스를 실행중이거나..등)
- Blocked: 대기 상태에서는 프로세스가 다른 event를 기다리는 동안 프로세스의 수행을 중단시키는 것(프로세스가 디스크에 대한 입출력을 요청하였을때..등)




