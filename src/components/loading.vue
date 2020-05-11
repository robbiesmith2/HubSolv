<template>
    <div class="loading">
        <div class="loading__wrapper">
            <span class="loading__dot"></span>
            <span class="loading__dot"></span>
            <span class="loading__dot"></span>
            <span class="loading__dot"></span>
        </div>
        <p>Loading</p>
    </div>
</template>

<script>
export default {
    name: 'loading'
}
</script>

<style lang="scss" scoped>

    $duration: 1.2;

    @keyframes bounce {
        0% {
            transform: translateY(0) scale(1);
        }
        10% {
            transform: translateY(0) scale(1.3);
        }
        20%, 100% {
            transform: translateY(0) scale(1);
        }
    }

    .loading {
        margin: 2rem 0;
        
        &__wrapper {
            display: inline-grid;
            grid-column-gap: 0.5rem;
            grid-template-columns: 1fr 1fr 1fr 1fr;
            justify-content: center;
            align-items: center;
        }

        &__dot {
            content: '';
            width: 10px;
            height: 10px;
            background: #2980b9;
            border-radius: 50%;
            animation: bounce #{$duration}s infinite ease-in-out;

            @for $i from 0 through 4 {
                &:nth-child(#{$i}) {
                        animation-delay: #{$i * 0.1}s;
                    }
                
            }
        }
    }
</style>