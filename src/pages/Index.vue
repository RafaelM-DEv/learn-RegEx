<template>
  <q-page class="regex column items-center">
    <q-card class="regex__card text-white q-mt-lg ">
      <q-card-section>
        <h1>RegEx</h1>
        <h4>O que é uma expressão regular?</h4>
        <div>Uma expressão regular é um método formal de se especificar um padrão de texto.</div>
        <div>Com ela podemos lidar com as seguintes situações:</div>
        <ul>
          <li>procura</li>
          <li>substituição</li>
          <li>validação de formatos</li>
          <li>filtragem de informações</li>
        </ul>
      </q-card-section>
    </q-card>
    <q-tabs v-model="tab" class="text-teal regex__section">
        <q-tab name="regex" icon="favorite" label="Primeiros Passos" />
        <q-tab name="javascript" icon="code" label="Usando no JavaScript" />
    </q-tabs>
    <q-tab-panels v-model="tab" class="regex__panels  shadow-3">
      <q-tab-panel name="regex">
        <section class="column text-white ">
          <div>
            <h5>Criando nossas primeiras RegEx</h5>
            <p>Usando javascript podemos optar por duas formas de se criar uma regex.</p>
            <p>Podemos criar usando um <strong>constructor</strong> :</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex = new RegExp ('dog', 'gi')
            </div>
            <p>Ou criando de forma <strong>literal</strong> :</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex = /dog/gi
            </div>
            <p>Exemplo prático:</p>
            <p>Buscando apenas uma letra.(escreva uma palavra ou a letra que buscamos)</p>
            <q-input v-model="text" type="text" color="white" outlined dense label="Pattern: /a/" :bg-color="regTestCaractere"/>
            <div class="q-mt-sm">match: {{ text.match(/a/) }}</div>
            <p>Perceba que se tentar digitar "A" maiúsculo não terá o match, isso é porque temos case sensitive em nossas regex,
              para termos controle sobre isso usamos a flag <strong>"i"</strong>. Vamos ver isso logo em seguida.</p>
          </div>

          <div>
            <h5>Flags</h5>
            <p>Elas adicionam comportamentos adicionais a nossas regras, como:</p>
            <ul>
              <li>g - Achar todas as ocorrências da regex</li>
              <li>i - ignora case sensitive</li>
              <li>m - multilinha, lida com caracrteres de inicio e fim (^ e $) ao operar em múltiplas linhas</li>
            </ul>
            <p>Exemplo prático:</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex = /dog/g
            </div>
            <div class="row no-wrap q-gutter-x-sm">
              <q-input v-model="patternFlag" type="text" outlined dense label="Pattern" bg-color="white" class="q-mb-sm col-10" />
              <q-input v-model="flag" type="text" outlined dense label="Flag" bg-color="white" class="q-mb-sm" />
            </div>
            <q-input v-model="textFlag" :type="inputTypeMode(this.flag)" outlined dense :label="'Pattern: /' + patternFlag + '/' + flag"
                     :bg-color="regTestFlag" color="white"/>
            <div class="q-mt-sm">match: {{ textFlag.match(match) }}</div>
          </div>

          <div>
            <h5>Operador pipe "|"</h5>
            <p>Algumas vezes precisamos dar match em mais de um termo, para isso usamos o operador pipe "|" </p>
            <p> Ele funciona basicamente como nosso operador lógico <strong>OR</strong> "| |" .</p>
            <p>Exemplo prático:</p>
            <q-input v-model="textPipe" type="text" outlined dense label="Pattern: /ver|distrai/g " :bg-color="regTestPipe" color="white"/>
            <div class="q-mt-sm">match: {{ textPipe.match(/ver|distrai/g) }}</div>
          </div>

          <div>
            <h5>Conjuntos " [ ] "</h5>
            <p>Com os conjuntos dizemos a regex que uma determinada casa pode ter diversos valores</p>
            <p>Uma funcionalidade interessante é de adicionar range (invervalos) dentro dos nossos conjuntos.</p>
            <p>Podemos determinar um conjunto de match em letras que vão de A à Z ou pegue qualquer digito (0 à 9).</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
            const regex =  /[a-z]/g
            </div>
            <p>Exemplo prático:</p>
            <div class="row no-wrap q-gutter-x-sm">
              <q-input v-model="patternInterval" type="text" outlined dense label="Pattern" bg-color="white" class="q-mb-sm col-10" />
              <q-input v-model="flagInterval" type="text" outlined dense label="Flag" bg-color="white" class="q-mb-sm" />
            </div>
            <q-input v-model="textInterval" :type="inputTypeMode(this.flagInterval)" outlined dense :label="'Pattern: /' + patternInterval + '/' + flagInterval"
                     :bg-color="regTestInterval" color="white"/>
            <div class="q-mt-sm">match {{ textInterval.match(matchInterval)}}</div>
          </div>

          <div>
            <h5>Metacaracteres</h5>
            <p>Um metacaractere bastante recorrente é o ponto . , ele funciona como um coringa, sendo capaz de dar match em qualquer caractere.</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex = /cas./gi
            </div>
            <p>Se desejar pegar a forma literal do caractere basta usar o <strong>escape</strong> "\"</p>
            <p>Exemplo prático:</p>
            <div class="row no-wrap q-gutter-x-sm">
              <q-input v-model="patternMeta" type="text" outlined dense label="Pattern" bg-color="white" class="q-mb-sm col-10" />
              <q-input v-model="flagMeta" type="text" outlined dense label="Flag" bg-color="white" class="q-mb-sm" />
            </div>
            <q-input v-model="textMeta" :type="inputTypeMode(this.flagMeta)" outlined dense :label="'Pattern: /' + patternMeta + '/' + flagMeta" :bg-color="regTestMeta" color="white"/>
            <div class="q-mt-sm">match: {{ textMeta.match(matchMeta)}}</div>
          </div>

          <div>
            <h5>shorthands</h5>
            <p>Para simplificar a escrita e leitura das regex, possuímos algumas shorthands que são extremamente úteis para deixar ainda mais claro nosso código.</p>
            <p>Veja como podemos escrever esse conjunto [0-9] para \d ,[a-zA-Z0-9_] para \w ou para tratar espaços em branco [\r\n\t\f\v ] para \s simplificando ainda mais nossas regras.</p>
            <p>Exemplo prático:</p>
            <q-input v-model="textShort" type="text" outlined dense label="Pattern: /\w\w\w\w\w@\w\w\.com/" :bg-color="regTestShort" color="white"/>
            <div class="q-mt-sm">match: {{textShort.match(/\w\w\w\w\w\w@\w\w\.com/)}}</div>
          </div>

          <div>
            <h5>Quantificadores</h5>
            <p>Uma maneira de deixar suas regras ainda mais simples é com o uso dos quantificadores. Com eles podemos dizer quantas vezes uma mesma regra pode aparecer em sequência.</p>
            <ul>
              <li>? - zero ou uma ocorrência</li>
              <li>* - zero ou mais ocorrências</li>
              <li>+ - uma ou mais ocorrências</li>
              <li>{n, m} - de n até m</li>
            </ul>
            <p>Digamos que queremos pegar um documento como o cpf, que contêm muitos números e pontuações (. e -) onde a validação pode aceitar o cpf com e sem pontuação.</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
            const regex =  /\d{3}\.?\d{3}\.?\d{3}-?\d{2}/
            </div>
            <p>Exemplo prático:</p>
            <div class="row no-wrap q-gutter-x-sm">
              <q-input v-model="patternQuant" type="text" outlined dense label="Pattern" bg-color="white" class="q-mb-sm col-10" />
              <q-input v-model="flagQuant" type="text" outlined dense label="Flag" bg-color="white" class="q-mb-sm" />
            </div>
            <q-input v-model="textQuant" :type="inputTypeMode(this.flagQuant)" outlined dense :label="'Pattern: /' + patternQuant + '/' + flagQuant" :bg-color="regTestQuant" color="white"/>
            <div class="q-mt-sm">match: {{ textQuant.match(matchQuant)}}</div>
          </div>

          <div>
            <h5>Âncoras</h5>
            <p>Muitas vezes vamos precisar delimitar a ação da nossa regex. Desse modo podemos usar três metas para nos auxiliar nessa função.</p>
            <p>Quando queremos tratar uma palavra que em suas extremidades não possua outra letra ou palavra, usamos a shorthands \b (Corresponde a um limite de palavras, isto é, a posição entre uma palavra e um espaço.).</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex = /\bpar\b/gi
            </div>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /\bpar[a-z]+/gi
            </div>
            <p>Exemplo prático:</p>
            <div class="row no-wrap q-gutter-x-sm">
              <q-input v-model="patternAncora" type="text" outlined dense label="Pattern" bg-color="white" class="q-mb-sm col-10" />
              <q-input v-model="flagAncora" type="text" outlined dense label="Flag" bg-color="white" class="q-mb-sm" />
            </div>
            <q-input v-model="textAncora" :type="inputTypeMode(this.flagAncora)" outlined dense :label="'Pattern: /' + patternAncora + '/' + flagAncora" :bg-color="regTestAncora" color="white"/>
            <div class="q-mt-sm">match: {{ textAncora.match(matchAncora)}}</div>
            <div class="text-italic text-grey-5 q-my-sm" style="box-shadow: -3px 0px 0px #e76f51">
              Vale notar que caracteres com acentos ou - são considerados bordas.
            </div>
            <p>Podemos lidar com o início e fim de uma linha. Usamos a meta ^ para indicar o início de uma linha e $ indicando o fim de uma linha. Algo importante a se notar é que para as âncoras funcionarem a cada quebra de linha \n a flag m tem que estar habilitada.</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /^[a-z]*\b/gmi
            </div>
            Confira com o uso do meta $ em uma estrofe:
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /[a-z]+nto$/gmi
            </div>
            Conseguimos tratar início e final de um texto ao mesmo tempo. veja:
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /^https:\/\/w{3}\.[a-z]+\.com$/gmi
            </div>
            <p>Exemplo prático:</p>
            <div class="row no-wrap q-gutter-x-sm">
            <q-input v-model="patternAncoraLine" type="text" outlined dense label="Pattern" bg-color="white" class="q-mb-sm col-10" />
              <q-input v-model="flagAncoraLine" type="text" outlined dense label="Flag" bg-color="white" class="q-mb-sm" />
            </div>
            <q-input v-model="textAncoraLine" :type="inputTypeMode(this.flagAncoraLine)" outlined dense :label="'Pattern: /' + patternAncoraLine + '/' + flagAncoraLine" :bg-color="regTestAncoraLine" color="white"/>
            <div class="q-mt-sm">match: {{ textAncoraLine.match(matchAncoraLine) }}</div>
          </div>

          <div>
            <h5>Grupos "( )"</h5>
            <p>Por fim, temos os grupos que facilita ainda mais nossas regras. Eles nos possibilita a criação de regras isoladas, possibilita a criação de referencias (retrovisores) para o reuso da mesma regra em outro local dentro de uma mesmo regex e ainda cria a possibilidade de validações dentro da regex.</p>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
            const regex =  /(\d{2})\/?(\d{2})?\/(\d{4})/
            </div>
            Podemos definir grupos que podem ser ignorados (non-capturing groups) na hora do match usando a sintaxe (?:).
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /([a-z]*)\s(?:ronaldo)/gi
            </div>
            Com os grupos podemos criar grupos aninhados (grupos dentro de grupos).
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /((d[io])|(co))([a-z]{2})(do)/gi
            </div>
            Os grupos possuem grupos especiais. Como o positive lookahead (?=) e o seu oposto, negative lookahead (?!). Com o positive lookahead podemos verificar se existe um grupo a frente de uma expressão ou grupo.
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /([a-z]+)(?=,)/gi
            </div>
            <div class="bg-grey-3 q-pa-sm q-mb-md text-black">
              const regex =  /([a-z]+)(?!,)\b/gi
            </div>
            <p>Exemplo prático:</p>
            <div class="row no-wrap q-gutter-x-sm">
              <q-input v-model="patternGroup" type="text" outlined dense label="Pattern" bg-color="white" class="q-mb-sm col-10" />
              <q-input v-model="flagGroup" type="text" outlined dense label="Flag" bg-color="white" class="q-mb-sm" />
            </div>
            <q-input v-model="textGroup" :type="inputTypeMode(this.flagGroup)" outlined dense :label="'Pattern: /' + patternGroup + '/' + flagGroup" :bg-color="regTestGroup" color="white"/>
            <div class="q-mt-sm">match: {{ textGroup.match(matchGroup) }}</div>
          </div>
        </section>
      </q-tab-panel>
      <q-tab-panel name="javascript">
        <section class=" column text-white ">
          <h5>Métodos de regex no js</h5>
          <p>O objeto regex possui dois métodos: exec e test. Já com string possui 4 métodos: match, replace, search e split. Porém neste post vou me ater somente a 3 métodos: test, match e replace.</p>
          <div>
            <h5>test</h5>
            <p>Usado para verificar se uma regex da match com uma string. Ela retorna sempre valor boolean. Este método é ideal para fazer validações como por exemplo validar se um email, telefone ou data estão corretos.</p>
            <iframe width="100%" height="300" src="//jsfiddle.net/Far3ll/qh4ao68r/embedded/js/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
          </div>
          <div>
            <h5>match</h5>
            <p>Ele retorna um array, com as string que deram match com a regex. Se não houver valor, ele retorna null. Vejamos um exemplo procurando cep validos em um texto:</p>
            <iframe width="100%" height="300" src="//jsfiddle.net/Far3ll/j7qr925c/embedded/js/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
            <p>Vejamos acima que o último número não foi pego no match, pois ele não é um cep válido.</p>
          </div>
          <div>
            <h5>replace</h5>
            <p>Usado para substituir strings que deram match por uma nova string. Segue um exemplo:</p>
            <iframe width="100%" height="300" src="//jsfiddle.net/Far3ll/jxdvpob4/1/embedded/js/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
          </div>
        </section>
      </q-tab-panel>
    </q-tab-panels>
    <q-page-sticky position="bottom-right" :offset="[18, 18]">
      <q-btn push icon="expand_less" color="orange-4" @click="toTop" />
    </q-page-sticky>
  </q-page>
</template>

<script>
export default ({
  data () {
    return {
      patternFlag: '',
      flag: '',
      textFlag: '',

      patternInterval: '',
      flagInterval: '',
      textInterval: '',

      patternMeta: '',
      flagMeta: '',
      textMeta: '',

      patternQuant: '',
      flagQuant: '',
      textQuant: '',

      patternAncora: '',
      flagAncora: '',
      textAncora: '',

      patternAncoraLine: '',
      flagAncoraLine: '',
      textAncoraLine: '',

      patternGroup: '',
      flagGroup: '',
      textGroup: '',

      regra: '',
      text: '',
      textPipe: '',
      textShort: '',
      tab: 'regex'
    }
  },

  computed: {
    match () {
      const regex = new RegExp(this.patternFlag, this.flag)
      return regex
    },

    matchGroup () {
      const regex = new RegExp(this.patternGroup, this.flagGroup)
      return regex
    },

    matchInterval () {
      const regex = new RegExp(this.patternInterval, this.flagInterval)
      return regex
    },

    matchMeta () {
      const regex = new RegExp(this.patternMeta, this.flagMeta)
      return regex
    },

    matchQuant () {
      const regex = new RegExp(this.patternQuant, this.flagQuant)
      return regex
    },

    matchAncora () {
      const regex = new RegExp(this.patternAncora, this.flagAncora)
      return regex
    },

    matchAncoraLine () {
      const regex = new RegExp(this.patternAncoraLine, this.flagAncoraLine)
      return regex
    },

    regTestCaractere () {
      return /a/.test(this.text) ? 'green' : 'red-5'
    },

    regTestFlag () {
      const regex = new RegExp(this.patternFlag, this.flag)
      return regex.test(this.textFlag) ? 'green' : 'red-5'
    },

    regTestPipe () {
      return /ver|distrai/g.test(this.textPipe) ? 'green' : 'red-5'
    },

    regTestInterval () {
      const regex = new RegExp(this.patternInterval, this.flagInterval)
      return regex.test(this.textInterval) ? 'green' : 'red-5'
    },

    regTestMeta () {
      const regex = new RegExp(this.patternMeta, this.flagMeta)
      return regex.test(this.textMeta) ? 'green' : 'red-5'
    },

    regTestShort () {
      return /\w\w\w\w\w\w@\w\w\.com/.test(this.textShort) ? 'green' : 'red-5'
    },

    regTestQuant () {
      const regex = new RegExp(this.patternQuant, this.flagQuant)
      return regex.test(this.textQuant) ? 'green' : 'red-5'
    },

    regTestAncora () {
      const regex = new RegExp(this.patternAncora, this.flagAncora)
      return regex.test(this.textAncora) ? 'green' : 'red-5'
    },

    regTestAncoraLine () {
      const regex = new RegExp(this.patternAncoraLine, this.flagAncoraLine)
      return regex.test(this.textAncoraLine) ? 'green' : 'red-5'
    },

    regTestGroup () {
      const regex = new RegExp(this.patternGroup, this.flagGroup)
      return regex.test(this.textGroup) ? 'green' : 'red-5'
    }
  },

  methods: {
    inputTypeMode (model) {
      const regex = /m/g
      return regex.test(model) ? 'textarea' : 'text'
    },

    toTop () {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }
  }
})
</script>

<style lang="scss">
.regex {
  font-family: Poppins;
  background-image: linear-gradient(to top, #264653, #e76f51);

  &__card {
    background-color: #e9c46a;
    width: 80%;
    z-index: 1;
  }

  &__section {
    background-color: #264653;
    padding: 20px;
    width: 80%;
  }

  &__panels {
    background-color: #264653;
    padding: 20px;
    width: 80%;
    box-shadow: 0 -1px 3px rgba($color: #000000, $alpha: 0.5);
  }
}

h1 {
  height: 110px;
  background-color: #ff0044;
  font-weight: 700;
  background-image: linear-gradient(-75deg, transparent 0, transparent 5%, rgba(255,255,255,0.5) 5%, rgba(255,255,255,0.5) 10%, transparent 10%, transparent 100%);
  background-size: 200% 100%;
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
  animation: shine 1s ease-in-out infinite;
}

@keyframes shine {
  0% { background-position: 0%; }
  100% { background-position: -150%; }
}
</style>
