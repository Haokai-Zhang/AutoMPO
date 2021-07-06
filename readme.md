## AutoMPO

”Generate matrix product operator automatically based on finite state automata. “

### Small Tutorial

Use "fsa.Add()" to add each term in your Hamiltonian.

Use "fsa.GenMPO()" to generate a matrix product form of the Hamiltonian.

Test file for the transverse-field Ising chain.

```Python
from AutoMPO.class_fsa import fsa
from AutoMPO.class_named_data import named_data
from AutoMPO.opr_pool import GenSpinOpr

if __name__ == "__main__":
    # model parameter
    N = 5
    J = 1
    g = 0.5
    # define operator with a string as name
    Sz = named_data('Sz', GenSpinOpr('Sz'))
    Sx = named_data('Sx', GenSpinOpr('Sx'))
    # construct finite state automata
    fsa = fsa(N)
    for i in range(0, N):
        # add each term in the Hamiltonian
        if (i < N - 1):
            fsa.Add(J, [Sz, Sz], [i, i + 1])
        fsa.Add(g, [Sx], [i])
    # use the constructed fsa to generate MPO
    list_mpo = fsa.GenMPO()
    # visualize MPO represented by operator symbols
    fsa.PrintSymbolMPO()
```

Click [here](https://zhuanlan.zhihu.com/p/382361509) for the general idea behind AutoMPO.

Click [here](https://zhuanlan.zhihu.com/p/385274056) for the implementation details of AutoMPO.

Click [here](https://www.zhihu.com/question/270191605/answer/1585609137) for more information about the density matrix renormalization group (DMRG) method. 

