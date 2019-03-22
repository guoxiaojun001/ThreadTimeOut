# ThreadTimeOut
多线程超时问题


Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try {
                System.out.println(Thread.currentThread());
                Thread.sleep(6000);
            } catch (InterruptedException e) {
                e.printStackTrace();
                return;
            }
            System.out.println("任务继续执行..........");
        }
    });
    
    System.out.println(Thread.currentThread());
    thread.start();
    //精华在于这句话
    TimeUnit.SECONDS.timedJoin(thread, 3);
    
    if (thread.isAlive()) {
        thread.interrupt();
        throw new TimeoutException("Thread did not finish within timeout");
    }
