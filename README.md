# Projeto-PingPongCollor
Game feito a partir de um tutorial

>>BOLA

public class ball : MonoBehaviour
{

    public float vel = 30;

    public GameObject paredeEsq;

    void Start()
    {
        GetComponent<Rigidbody2D>().velocity = Vector2.right * vel;
    }

    float hit(Vector2 ballPos, Vector2 racketPos, float racketHeight)
    {
        return (ballPos.y - racketPos.y) / racketHeight;
    }

    void OnCollisionEnter2D(Collision2D col)
    {
        //acertou a racket esquerda ?
        if (col.gameObject.name == "racketEsq")
        {
            //cacular 'hit'
            float y = hit(transform.position, col.transform.position, col.collider.bounds.size.y);

            //calcular direção 
            Vector2 dir = new Vector2(1, y).normalized;

            //setar a velocidade
            GetComponent<Rigidbody2D>().velocity = dir * vel;
        }

        //acertou a racket esquerda ?
        if (col.gameObject.name == "racketDir")
        {
            //cacular 'hit'
            float y = hit(transform.position, col.transform.position, col.collider.bounds.size.y);

            //calcular direção 
            Vector2 dir = new Vector2(-1, y).normalized;

            //setar a velocidade
            GetComponent<Rigidbody2D>().velocity = dir * vel;
        }
    }
}

>>RAQUETES

public class rackets : MonoBehaviour {
   
    public float vel = 30;
    public string eixo = "Vertical";

    void Update()
    {
        float v = Input.GetAxisRaw(eixo);
        GetComponent<Rigidbody2D>().velocity = new Vector2(0, v) * vel;
    }
}
